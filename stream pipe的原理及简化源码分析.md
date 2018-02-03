# 前言
> 在编写代码时，我们应该有一些方法将程序像连接水管一样连接起来 -- 当我们需要获取一些数据时，可以去通过"拧"其他的部分来达到目的。这也应该是IO应有的方式。 -- Doug McIlroy. October 11, 1964

本质上来说，编码就是对数据的读取，处理最后返回结果，数据在一个程序又一个程序中不断传递。理想情况下，数据的传递应该是不停滞的，但是现实情况中因为诸如单个数据过大，内存较小，IO处理较慢等客观原因使数据不能流畅的`流动`起来。这时我们就需要一种方法去将数据拆分成一小块一小块的数据(chunks),流水一样的读取处理写入。这种方法便是`流(stream)`，nodejs中的流主要分为以下四种：
* Readable（可读流）
* Writable（可写流）
* Duplex（可读写流）
* Transform (变换流)

而所有的流都有一种公有方法，它会像管道一样处理流的数据，这便是`pipe`,下面一张大神制作的图很好的演示了这个过程：
![Markdown](http://i4.bvimg.com/628954/8a191ee898d6f7e5.gif)

#正文

### pipe期望的使用方式
`pipe`函数需要将源头`src`并将数据输出到一个可写的流`dst`中：

```javascript
src.pipe(dst)
```
`pipe`将会返回`dst`,所以我们希望可以链式调用将多个流用管道连接起来:

```javascript
a.pipe(b).pipe(c).pipe(d)
```

### pipe的简化源码分析
为了实现以上期望的使用方式，我们将Nodejs源码简化一下看是怎样实现的
```javascript
stream.prototype.pipe = function(dest, options) {
  this.on('data', (chunk) => {
    if (dest.writable) {
      if (false === dest.write(chunk) && this.pause) {
        this.pause();
      }
    }
  });
  dest.on('drain', () => {
    this.resume();
  });
  dest.emit('pipe', this);
  
  return dest;
};
```

以上代码主要做了4件事：
* 可读流监听`data`事件
  1）首先判断`dest.Writable`，当写完时会赋值为false
  2）此时如果消费者消费速度慢，这时产生了一个现象，叫做`背压`。背压问题即是外部的生产者和消费者速度差造成的，此时我们需要暂停写入`.pause()`
* 可写流监听`drain`事件
  1）消费者完成消费，可以触发`drain`事件，此时我们可以继续向流中写入数据。执行`.resume()`
* 触发`pipe`事件，通知有流写入
* 返回`dest`流，可以进行链式调用

### 小记
简单的梳理了下stream pipe的原理和实现方式。在现实应用中诸如gulp，Browserify等工作流工具都使用了pipe。而stream更是应用广泛，文件、http、打包压缩甚至console等都是用流实现的。

###### 参考资料
* [gulp源码解析（一）—— Stream详解s](http://www.cnblogs.com/vajoy/p/6349817.html)
* [stream-handbook](https://github.com/jabez128/stream-handbook)


