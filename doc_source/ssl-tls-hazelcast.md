# Configuring SSL/TLS for Hazelcast<a name="ssl-tls-hazelcast"></a>

[Transport Layer Security](https://en.wikipedia.org/wiki/Transport_Layer_Security) \(TLS\) is a cryptographic protocol designed to provide communications security over a computer network\.

With Hazelcast you can encrypt socket level communication between Hazelcast members and between Hazelcast clients and members, for end to end encryption\.

EnginFrame ships with Hazelcast Open Source which doesn't support the [security suite](https://hazelcast.com/product-features/feature-comparison/) that includes SSL/TLS asymmetric encryption\.

## Setup SSL/TLS communication with Hazelcast Enterprise<a name="ssl-tls-hazelcast-setup"></a>

1. To learn how to set up SSL/TLS communication with Hazelcast Enterprise, you need:
   + A valid Hazelcast Enterprise [license](https://issues.amazon.com/issues/(https://hazelcast.com/trial-request/)\.
   + The Hazelcast Enterprise [jar](https://repository.hazelcast.com/release/com/hazelcast/hazelcast-enterprise/5.1.1/hazelcast-enterprise-5.1.1.jar) \(current version 5\.1\.1\.

1. To begin, replace `${EF_ROOT}/WEBAPP/WEB-INF/lib/hazelcast-5.1.1.jar` with the downloaded Hazelcast Enterprise `jar`\.

1. After the `jar` is replaced, update the Hazelcast configuration file `${EF_ROOT}/conf/hazelcast.xml` with the license key that you already obtained by following this [guide](https://docs.hazelcast.com/hazelcast/5.1/getting-started/install-enterprise#installing-an-enterprise-license-key)\.

1. Implement `com.hazelcast.nio.ssl.SSLContextFactory` and configure the SSL section in the network configuration\. Hazelcast provides a default `SSLContextFactory`, `com.hazelcast.nio.ssl.BasicSSLContextFactory`, that uses the keystore to initialize SSLContext\. An example configuration for TLS/SSL follows:

   ```
   <hazelcast>
   ...
   <network>
        ...
        <ssl enabled="true">
           <factory-class-name>
               com.hazelcast.nio.ssl.BasicSSLContextFactory
           </factory-class-name>
           <properties>
               <property name="protocol">TLSv1.2</property>
               <property name="mutualAuthentication">REQUIRED</property>
               <property name="keyStore">/efs/KeyStore.jks</property>
               <property name="keyStorePassword">passphrase</property>
               <property name="keyStoreType">JKS</property>
               <property name="trustStore">/efs/truststore.jks</property>
               <property name="trustStorePassword">passphrase</property>
               <property name="trustStoreType">JKS</property>
           </properties>
        </ssl>
   </network>
   ...
   </hazelcast>
   ```

**Property descriptions:**
   + **keyStore**: Path of your keystore file\.
   + **keyStorePassword**: Password to access the key from your keystore file\.
   + **keyManagerAlgorithm**: Name of the algorithm based on the provided authentication keys\.
   + **keyStoreType**: Type of the keystore\. Its default value is JKS\. Another commonly used type is the PKCS12\. Available keystore/truststore types depend on your operating system and Java runtime\.
   + **trustStore**: Path of your truststore file\. The truststore file is a keystore file that contains a collection of certificates trusted by your application\.
   + **trustStorePassword**: Password to unlock the truststore file\.
   + **trustStoreType**: Type of the truststore\. Its default value is JKS\. Another commonly used type is the PKCS12\. Available keystore/truststore types depend on your operating system and Java runtime\.
   + **mutualAuthentication**: Mutual authentication configuration\. It’s empty by default which means the client side of connection is not authenticated\. Available values are:
     + REQUIRED \- server forces usage of a trusted client certificate\.
     + OPTIONAL \- server asks for a client certificate, but doesn’t require it\.

   For more information, see the [Hazelcast documentation](https://docs.hazelcast.com/hazelcast/latest/security/tls-ssl)\.

1. Follow the next example to properly configure a Keystore and a Truststore that leverages both `keytool` and `openssl` \.

   ```
   $ keytool cd /efs
   keytool -genkey -alias bmc -keyalg RSA -keystore KeyStore.jks -keysize 2048
   openssl req -new -x509 -keyout ca-key -out ca-cert
   keytool -keystore KeyStore.jks -alias bmc -certreq -file cert-file
   openssl x509 -req -CA ca-cert -CAkey ca-key -in cert-file -out cert-signed -days 365 -CAcreateserial -passin pass:passphrase
   keytool -keystore KeyStore.jks -alias CARoot -import -file ca-cert
   keytool -keystore KeyStore.jks -alias bmc -import -file cert-signed
   keytool -keystore truststore.jks -alias bmc -import -file ca-cert
   ```

   With this example, you create a custom CA with `openssl` that's used to sign the Hazelcast certificate\. We recommend that you use a publicly available CA for production and reserve the use of custom CA certificates for testing purposes\.

1. Restart EnginFrame to leverage SSL/TLS for Hazelcast members and clients communications\.