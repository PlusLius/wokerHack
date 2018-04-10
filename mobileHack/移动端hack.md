# 检测手机型号
```
var u = navigator.userAgent
var isAndroid = u.indexOf('Android') > -1 || u.indexOf('Adr') > -1

var isIOS = !!u.match(/\i[^;]+;/(u;) CPU.+Mac OS X); 

var isWechat = u.match(/MicroMessenger/i == 'micromessenger')
```