# flutter_v2ray

[![Open Source Love](https://badges.frapsoft.com/os/v1/open-source.svg?v=103)](#)
![](https://img.shields.io/github/license/blueboy-tm/flutter_v2ray)
![](https://img.shields.io/github/stars/blueboy-tm/flutter_v2ray) ![](https://img.shields.io/github/forks/blueboy-tm/flutter_v2ray) ![](https://img.shields.io/github/tag/blueboy-tm/flutter_v2ray) ![](https://img.shields.io/github/release/blueboy-tm/flutter_v2ray) ![](https://img.shields.io/github/issues/blueboy-tm/flutter_v2ray)


## Table of contents
+ [Change logs](#change-logs)
+ [Features](#features)
+ [Supported Platforms](#supported-platforms)
+ [Get started](#get-started)
    * [Add dependency](#add-dependency)
    * [Examples](#examples)
        * [URL Parser](#url-parser)
        * [Edit Configuration](#edit-configuration)
        * [Making V2Ray connection](#making-v2ray-connection)
        * [More](#more-examples)
+ [Credits](#credits)
+ [Donation](#donation)


## Change logs
#### 1.0.1

* fix EventChannel crash
* add getServerDelay method

#### [see more](./CHANGELOG.md)

## Features
- Run V2Ray Proxy & VPN Mode
- Get Server Delay
- Parsing V2Ray sharing links and making changes to them

<br>

## Supported Platforms

| Platform  | Status    |
| --------- | --------- |
| Android   | Done ✅   |
| IOS       | Soon ❎   |
| Desktop   | Soon ❎   |

<br>

## Get started

### Add dependency

You can use the command to add flutter_v2ray as a dependency with the latest stable version:

```console
$ flutter pub add flutter_v2ray
```

Or you can manually add flutter_v2ray into the dependencies section in your pubspec.yaml:

```yaml
dependencies:
  flutter_v2ray: ^replace-with-latest-version
```

<br>

## Examples


### URL Parser

``` dart
import 'package:flutter_v2ray/flutter_v2ray.dart';

// v2ray share link like vmess://, vless://, ...
String link = "link_here";
V2RayURL parser = FlutterV2ray.parseFromURL(link);

// Remark of the v2ray
print(parser.remark);

// generate full v2ray configuration (json)
print(parser.getFullConfiguration());
```
### Edit Configuration
``` dart
// Change v2ray listening port
parser.inbound['port'] = 10890;
// Change v2ray listening host
parser.inbound['listen'] = '0.0.0.0';
// Change v2ray log level
parser.log['loglevel'] = 'info';
// Change v2ray dns
parser.dns = {
    "servers": ["1.1.1.1"]
};
// and ...

// generate configuration with new settings
parser.getFullConfiguration()
```

<br>

### Making V2Ray connection
``` dart
import 'package:flutter_v2ray/flutter_v2ray.dart';

final FlutterV2ray flutterV2ray = FlutterV2ray(
    onStatusChanged: (status) {
        // do something
    },
);

// You must initialize V2Ray before using it.
await flutterV2ray.initializeV2Ray();



// v2ray share link like vmess://, vless://, ...
String link = "link_here";
V2RayURL parser = FlutterV2ray.parseFromURL(link);


// Get Server Delay
print('${flutterV2ray.getServerDelay(config: parser.getFullConfiguration())}ms');

// Permission is not required if you using proxy only
if (await flutterV2ray.requestPermission()){
    flutterV2ray.startV2Ray(
        remark: parser.remark,
        // The use of parser.getFullConfiguration() is not mandatory,
        // and you can enter the desired V2Ray configuration in JSON format
        config: parser.getFullConfiguration(),
        blockedApps: null,
        proxyOnly: false,
    );
}

// Disconnect
flutterV2ray.stopV2Ray();
```

<br>

## More examples
- [Simple v2ray client written in flutter](https://github.com/blueboy-tm/flutter_v2ray/blob/master/example/lib/main.dart)

## Credits
[badvpn (tun2socks)](https://github.com/ambrop72/badvpn) Copyright (C) Ambroz Bizjak

All rights reserved.


## Donation
If you liked this package, you can support me with one of the following links.

### Buy me a coffee

<a href="https://www.buymeacoffee.com/bBUqA54Bhe" target="_blank"><img src="https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png" alt="Buy Me A Coffee" style="height: 41px !important;width: 174px !important;box-shadow: 0px 3px 2px 0px rgba(190, 190, 190, 0.5) !important;-webkit-box-shadow: 0px 3px 2px 0px rgba(190, 190, 190, 0.5) !important;" ></a>


### Cryptocurrency

+ BTC:
    * bc1qrtq0ygmxw7meak3ukvxn03za2j7t7s4uxuujct
+ Tron
    * TVQQdim3pxa4XoZyRRVHQ8GsY42rEgB4ow
+ USDT
    * TRC20
        * TVQQdim3pxa4XoZyRRVHQ8GsY42rEgB4ow
    * ERC20
        * 0xD5d931BB40F02Ed45172faebD805B3f0ba70Fe73
+ DogeCoin
    * DNFaHFzmUfeUB6NFgQX1sLn9q8kknTmKd8
