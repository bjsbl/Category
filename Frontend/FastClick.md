# FastClick
https://github.com/ftlabs/fastclick  
## 为什么存在延迟
从点击屏幕上的元素到触发元素的 click 事件，移动浏览器会有大约 300 毫秒的等待时间。为什么这么设计呢？ 因为它想看看你是不是要进行双击（double tap）操作。 导入 fastclick.js 即可减少这个时间差
## 兼容性
* Mobile Safari on iOS 3 and upwards
* Chrome on iOS 5 and upwards
* Chrome on Android (ICS)
* Opera Mobile 11.5 and upwards
* Android Browser since Android 2
* PlayBook OS 1 and upwards
## 不适用场景
* 桌面浏览器
* ><meta name="viewport" content="width=device-width, initial-scale=1">

## 使用方法
* <script type='application/javascript' src='/path/to/fastclick.js'></script>
* ``$(function() {FastClick.attach(document.body);});``