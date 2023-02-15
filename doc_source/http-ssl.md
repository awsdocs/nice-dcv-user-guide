# Configuring HTTPS<a name="http-ssl"></a>

 HTTPS, [Hypertext Transfer Protocol over Secure Socket Layer](http://en.wikipedia.org/wiki/Https), is a [URI scheme](http://en.wikipedia.org/wiki/URI_scheme) used for secure [HTTP](http://en.wikipedia.org/wiki/HTTP) connections\. 

HTTPS is a protocol that adds a layer of encryption to security\-sensitive communication such as payment transactions and corporate logons\. 

 During the installation process, EnginFrame installer has an option for Apache Tomcat® to use HTTPS instead of HTTP\. By default, EnginFrame installs with the option to use HTTP protocol in the Apache Tomcat® web server\. 

If you choose the HTTPS option, the installer automatically creates self\-signed certificates under the `$EF_TOP/conf/tomcat/conf/certs` directory\. It also configures the Apache Tomcat® connector to use HTTPS\. 

## Using signed certificates with EnginFrame<a name="tomcat-https-certificate"></a>

If self\-signed certificates aren't suitable for your needs or you already have valid certificates setup for an HTTPS web server, we recommend that you refer to the [Apache Tomcat® official documentation](https://tomcat.apache.org/tomcat-9.0-doc/ssl-howto.html) when configuring your web server to use your certificates\. 

Apache Tomcat® provides different setup procedures depending on the specific format of the available certificate\. 

For example, if using a PEM private key and PEM certificate, the key and certificate must be converted before they are handled by Java™ `keytool` and keystores\. This is the best practice that's recommended in the Apache Tomcat® documentation\. 

First, convert PEM key and certificate into PKCS12 format:

```
$ openssl pkcs12 -export -in <your_CA_signed_PEM_cert>
  -inkey <your_PEM_private.key> -out <your_certificate_name>.p12
  -name tomcat -chain -CAFile <your_root_CA_certificate>
```

Next, import the newly created PKCS12 certificate into a Java™ keystore file:

```
$ $JAVA_HOME/bin/keytool -importkeystore -deststorepass <password>
  -destkeypass <password> -destkeystore tomcat.keystore
  -srckeystore <exported_private_key_and_cert.p12> -srcstoretype PKCS12
  -srcstorepass <password> -alias tomcat
```

If your certificate authority \(CA\) has intermediate certificates, import them into the keystore file\. It's likely that your CA provides instructions on how to do this and how to name certificates\. For example, if a CA intermediate certificate is already in a format that's supported by Java™ `keytool`, you can import it this way:

```
$ $JAVA_HOME/bin/keytool -import -alias intermed -keystore tomcat.keystore
  -trustcacerts -file gd_intermediate.crt
```

You might also need to import the root CA certificate into the keystore if it doesn't come from one of the CAs whose root certificates are pre\-configured in the Java™ system\.

For more information about how to use the [keytool](https://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html) and [openssl](https://www.openssl.org/) commands, in the [Oracle Java SE Documentation](https://docs.oracle.com/javase/7/docs)\.