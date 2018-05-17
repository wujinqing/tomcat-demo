## server配置

### connector元素

**acceptCount**
> 当所有可接受处理请求的线程都被占用时，放入到队列里面的待处理的请求个数，当这个队列满了之后新接收到的请求将会被拒绝，默认值是100.

**port**
> TCP端口号，系统只允许一个服务对于同一个一个ip只能监听一个的端口号。如果设置为0，Tomcat将会为这个connector随机选择一个空闲的端口号。

**protocol**
> 协议，设置一个协议来处理发过来的请求，默认值是HTTP/1.1，它将自动选择使用基于Java NIO的connector或者基于APR/native的connector

可以显示的指定下面几种协议：
* org.apache.coyote.http11.Http11NioProtocol - non blocking Java NIO connector
* org.apache.coyote.http11.Http11Nio2Protocol - non blocking Java NIO2 connector
* org.apache.coyote.http11.Http11AprProtocol - the APR/native connector.

**URIEncoding**
> 设置字符编码，默认：UTF-8

**compression**
> 为了节省服务器的带宽使用HTTP/1.1 GZIP压缩，是否压缩，默认是"off" 可以设置为："on"，"off"，"force"，或者具体数字
> off：禁用压缩
> on: 启动压缩
> force：所有情况下都会压缩
> 数值：当数据的字节数大于这个值是将启动压缩
> 如果content-length值未知，compression又设置为了"on"或者更高级别，output将会被压缩。

**compressionMinSize**
> 当compression属性设置为"on"时，可以指定这个值来确定当数据多大时进行压缩，默认"2048"

**connectionTimeout**
> Connector将会等待的时间长度，当接收到一个连接，到接收到request URI line的时间。
> -1：表示永远不超时
> 默认60000毫秒 (即60 seconds)，但是标准的server.xml设置的默认值是20000毫秒 (即 20 seconds)
> 除非设置disableUploadTimeout属性为false，否则它也将会用于读取request body超时时间。

**executor**
> 指定线程池， 引用Executor元素

**keepAliveTimeout**
> 在关闭一个连接之前等待这个连接发送其他请求的等待时间，超过这个时间没有接收到新的请求，连接将会被关闭。
> 默认值将使用connectionTimeout属性值，设置为-1表示永远不超时

**maxConnections**
> 在任意时刻服务器将会接收和处理的最大连接数。当连接数到达这个值时，服务器会继续接收连接，但不会处理。
> 新的连接将会被一直阻塞，直到正在处理的连接数低于maxConnections，这时服务器又会再次开始接收和处理新的连接。

> 注意：
> 一旦连接数到达maxConnections，操作系统可能还会基于acceptCount属性的设置继续接收新的连接。
> 这个属性的默认值随着connector类型的不同有不同的默认值，对于NIO and NIO2默认值是10000， 对于APR/native默认值是8192
> -1 表示没有限制

**maxThreads**
> 设置处理请求的最大线程数(供内部线程池使用，如果使用了Executor元素指定的线程池，这个设置将被忽略)，
> 这个值也代表着服务器能同时处理请求的个数。

**minSpareThreads**
> 设置保持允许的最小线程个数。如果没有设置默认是10个。如果引用了Executor元素指定的线程池而不是内部线程池这个设置将无效。

**processorCache**
> 为了提高性能protocol处理器缓存Processor objects，这个设置指定了多少个对象可以被缓存, -1 表示没有限制， 默认200个，
> 如果没有使用Servlet 3.0 asynchronous processing，建议和maxThreads保持一致，如果使用了则要大于maxThreads


**useSendfile**
> 是否启用sendfile，默认true，启动了这个选项将会禁用compression功能。

**socket.directBuffer**
> 是否使用	direct ByteBuffers or java mapped ByteBuffers， 默认false，
> 如果要使用这个功能，必须分配一定的内存。提供这个参数指定：-XX:MaxDirectMemorySize=256m

**socket.appReadBufSize**
> 每个在Tomcat中打开的连接都会有一个与之关联的read ByteBuffer，这个属性就是用来设置这个buffer的大小的，
> 默认值是8192 bytes. 在低并发的情况下你可以提高这个值来缓存更多的数据，对于一个很长的keep alive connections连接，请减少这个值或者增加堆内存。

**socket.appWriteBufSize**
> 指定write ByteBuffer的缓冲区大小， 如果你不想要支持数以万计的并发，可以提高这个值， 默认值8192 bytes.这个值是非常低的

**socket.bufferPool**
> 缓存Nio2Channel objects个数，为了减少垃圾回收， 默认值500个


**socket.processorCache**
> 缓存SocketProcessor objects个数，为了减少垃圾回收， 默认值500个, -1 无限制， 0 不缓存

























































































