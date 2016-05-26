# Hammerjs
解决移动端常用手势事件，比如：点击、滑动、拖动、多点操作

# 事件类型
### pan (event,pointers,threshold,direction)
拖拽动作
* panstart：拖动开始
* panmove：拖动过程
* panend：拖动结束
* pancancel：拖动取消
* panleft：向左拖动
* panright：向右拖动
* panup：向上拖动
* pandown：向下拖动

### pinch (event,pointers,threshold)
多点放大缩小
* pinchstart：多点触控开始
* pinchmove：多点触控过程
* pinchend：多点触控结束
* pinchcancel：多点触控取消
* pinchin：多点触控时两手指距离越来越近
* pinchout:多点触控时两手指距离越来越远

>默认是禁用的，开启: hammertime.get('pinch').set({ enable: true });

### press (event,pointers,threshold,time)
相当于PC端的Click事件，最小按压时间为251ms，常用于手机上用的“复制、粘贴”等功能。
* pressup：点击事件离开时触发

### roate (event,pointers,threshold)
多点旋转
* rotatestart：旋转开始
* rotatemove：旋转过程
* rotateend：旋转结束
* rotatecancel：旋转取消

### swipe (event,pointers,threshold,direction,velocity)
左右上下滑动
* swipeleft：向左滑动
* swiperight：向右滑动
* swipeup：向上滑动
* swipedown：向下滑动

### tap(event,pointers,taps,interval,time,threshold,posThreshold)
类似click（待测）
* tap

#使用方法
``  var hammertime = new Hammer(myElement, myOptions);  
  hammertime.on('pan', function(ev) {  
	console.log(ev);  
});`` 
