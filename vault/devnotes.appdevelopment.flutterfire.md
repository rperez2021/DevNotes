---
id: TDaGv5HQGlBQI3IAL9ZZj
title: Flutterfire
desc: ''
updated: 1645321979880
created: 1645321021593
---
## Version Change

`flutter build` kept throwing an error regarding `minsdkversion` needing to be bumped up to version 19 from 16 which is what the flutter starter was setup initially but once firebase was added it required the bump up.

The `build.gradle` was found in `/root/android/app`