# Connecting to a NICE DCV session using URI<a name="using-connecting-uri"></a>

Using a URI automatically opens a locally installed NICE DCV client with information passed into from the URI\.

Within the URL field of your internet browser, enter the URI in this format: `dcv://hostname[:port]/[?authToken][#sessionId]`

**Example**  
For example, `dcv://203.0.113.1:8443/?authToken=e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855#1234567890abcdef0`

Your locally installed client will open with the information prepopulated\.

For more information, see [GetSessionConnectionData](https://docs.aws.amazon.com/dcv/latest/sm-dev/GetSessionConnectionData.html) in the [NICE DCV Session Manager Developer Guide](https://docs.aws.amazon.com/dcv/latest/sm-dev)