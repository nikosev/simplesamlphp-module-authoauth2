**Table of Contents**

- [WeChat Login](#wechat-login)
- [Usage](#usage)
  - [Recommended Config](#recommended-config)
- [Creating WeChat Website App](#creating-wechat-website-app)

# WeChat Login

WeChat Login is a WeChat OAuth2.0 authorized login system built based on the OAuth2.0 protocol standard.
You can find more info about the WeChat API [here](https://developers.weixin.qq.com/doc/oplatform/en/Website_App/WeChat_Login/Wechat_Login.html).

# Usage

## Recommended Config

Create a sub class of the generic `authsource` called `wechat`.
There is a Third-Party provider that provides Wechat OAuth 2.0 support for the PHP League's OAuth 2.0 Client. To install the WeChat provider you must execute the command `composer require oakhope/oauth2-wechat`.

```php
   //authsources.php
    'wechat' => [
        'authoauth2:OAuth2',
        'providerClass' => 'Oakhope\OAuth2\Client\Provider\WebProvider',
        'appid' => 'myAppId',
        'secret' => 'mySecret',
        'redirect_uri' => 'https://hostname/SSP_PATH/module.php/authoauth2/linkback.php',
        'attributePrefix' => 'wechat.',
        // 'scopes' => ['snsapi_login'],
        'scopeSeparator' => ',',
        'label' => 'wechat',
    ],
```

and if are using this with a SAML IdP then you can map the OAuth attributes to regular friendly names in your `authproc` section of `saml20-idp-hosted.php`.

```php
    // saml20-idp-hosted.php
    $metadata['myEntityId'] = [
        'authproc' => [
            // Convert wechat claims to ldap friendly names
            10 => [
                'class' => 'core:AttributeMap',
                'authoauth2:wechat2name'
            ],
        ],
    // other IdP config options
    ]
```

# Creating WeChat Website App

 Before accessing WeChat OAuth2.0 Login, you must register a developer account on the [WeChat Open Platform](https://open.weixin.qq.com/?lang=en), own an approved website app, and obtain the corresponding AppID and AppSecret. You can start the access process after your application for WeChat Login is approved.
