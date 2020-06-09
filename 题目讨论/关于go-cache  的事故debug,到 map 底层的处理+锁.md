### [HHF的技术博客](https://www.haohongfan.com/post/2020-03-11-go-cache/)

欢迎关注微信公众号《HHF技术博客》

- 我里面本地缓存用的go-cache, 谁知道用的有问题, 放的太多了, 把go-cache的问题引发出来了. ￼
- 啥bug
- 溢出了呗。
go cahce 不是map+读写吗
- 是的, 关键go-cache的整个一个大map, 他的定期清理map时, 会锁整个map, 如果这个map方的太多了, 就会遇到这个问题
- 他这个不合理。。
搞成分段map 是不是就更牛逼了
可以对标N核心 搞成多段map. 压力应该小很多。
- 听说bigcache, freecache是这么搞的, 不过我还没去看源码
- 我自己写的就是分段map...
没看其他源码。。。
分段map + cas +  双buff
map 更新的话，应该是 map 底层的mutex 导致的吧
- 嗯, 是的
- 因为dirty data 导致 mu.mutex
那这是 map自身的问题~ 性能有限
