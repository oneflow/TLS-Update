.Net
====

You must be using 4.0 or above. 

if using the sdk please get the latest version from nuget. 
https://www.nuget.org/packages/OneFlowSDK/

In 4.0 or 4.5 if not using the sdk, you need to manualy set the protocol.

```ServicePointManager.SecurityProtocol = SecurityProtocolType.Tls11;```

PHP
===

You need to ensure OpenSSL version of at least 1.0.1 is installed.

if using the sdk update to the latest verison. 
https://github.com/Oneflow/oneflow-sdk-php

You can check if PHP will work with the following script:

```
<?php

echo "\n";
echo "PHP VERSION: " . phpversion() . "\n";
echo "OPEN SSL VERSION: " . OPENSSL_VERSION_TEXT. "\n";

$params = array(
    'ssl' => array(
        'ciphers' => 'ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA384:DH-DSS-AES256-GCM-SHA384:DHE-DSS-AES256-GCM-SHA384:DH-RSA-AES256-GCM-SHA384:DHE-RSA-AES256-GCM-SHA384:DHE-RSA-AES256-SHA256:DHE-DSS-AES256-SHA256:DH-RSA-AES256-SHA256:DH-DSS-AES256-SHA256:ECDH-RSA-AES256-GCM-SHA384:ECDH-ECDSA-AES256-GCM-SHA384:ECDH-RSA-AES256-SHA384:ECDH-ECDSA-AES256-SHA384:AES256-GCM-SHA384:AES256-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA256:DH-DSS-AES128-GCM-SHA256:DHE-DSS-AES128-GCM-SHA256:DH-RSA-AES128-GCM-SHA256:DHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES128-SHA256:DHE-DSS-AES128-SHA256:DH-RSA-AES128-SHA256:DH-DSS-AES128-SHA256:ECDH-RSA-AES128-GCM-SHA256:ECDH-ECDSA-AES128-GCM-SHA256:ECDH-RSA-AES128-SHA256:ECDH-ECDSA-AES128-SHA256:AES128-GCM-SHA256:AES128-SHA256'
    )
);

$context = stream_context_create($params);
$fp = fopen('https://www.howsmyssl.com/a/check', 'rb', false, $context);
if (!$fp)   {
//          print_r($http_response_header);
    throw new Exception("Problem creating stream from $url, \n\t".implode("\n\t", error_get_last()));
}

$response = stream_get_contents($fp);
if ($response === false)    throw new Exception("Problem reading data from $url, $php_errormsg");

$json = json_decode($response);

echo "You are using TLS version: " . $json->tls_version . "\n";
echo "\n";
```
You should see TLS 1.2 and OpenSSL version of at least 1.0.1

Node.js
=======

Node uses OpenSSL. TLSv1.2 requires OpenSSL 1.0.1c or higher.

Can check to see if supported:
```$ node -e "var https = require('https'); https.get('https://www.howsmyssl.com/a/check', function(res){ console.log(res.statusCode) });"```

You should see a 200 which indicates yes.

Ruby
====

Ruby 2.0.0 or above is required to use the TLSv1.2 capability of the system supplied OpenSSL. 
OpenSSL 1.0.1c is the first version that supplies TLSv1.2. 
That is, both Ruby > 2.0.0 and OpenSSL > 1.0.1c are required.
Run bundle update to update your dependencies.

Python
======

Python uses the system supplied OpenSSL. TLSv1.2 requires OpenSSL 1.0.1c or higher.

Java
====

- version 5: Not supported, you will need to upgrade
- version 6 + 7: TLSv1.2 must be enable explicitly, can set via:  http://docs.oracle.com/javase/7/docs/api/javax/net/ssl/SSLContext.html
- version 8: TLSv1.2 is the default 



