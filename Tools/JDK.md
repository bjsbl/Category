# System.getProperty()
  System.getProperty | 说明   
------------|-----------------
java.version | Java 运行时环境版本 
java.vendor | Java 运行时环境供应商 
java.vendor.url | Java 供应商的 URL 
java.home | Java 安装目录
java.vm.specification.version | Java 虚拟机规范版本
java.vm.specification.vendor | Java 虚拟机规范供应商
java.vm.specification.name | Java 虚拟机规范名称
java.vm.version | Java 虚拟机实现版本
java.vm.vendor | Java 虚拟机实现供应商
java.vm.name | Java 虚拟机实现名称
java.specification.version | Java 运行时环境规范版本
java.specification.vendor | Java 运行时环境规范供应商
java.specification.name | Java 运行时环境规范名称
java.class.version | Java 类格式版本号
java.class.path | Java 类路径
java.library.path | 加载库时搜索的路径列表
java.io.tmpdir | 默认的临时文件路径
java.compiler | 要使用的 JIT 编译器的名称
java.ext.dirs | 一个或多个扩展目录的路径
os.name | 操作系统的名称
os.arch | 操作系统的架构
os.version | 操作系统的版本
file.separator | 文件分隔符（在 UNIX 系统中是“/”）
path.separator | 路径分隔符（在 UNIX 系统中是“:”）
line.separator | 行分隔符（在 UNIX 系统中是“/n”）
user.name | 用户的账户名称
user.home | 用户的主目录
user.dir | 用户的当前工作目录

# Thread
Java通过Executors提供四种线程池

                 Thread | 说明 
------------------------|------------------------
newCachedThreadPool     | 创建一个可缓存线程池，如果线程池长度超过处理需要，可灵活回收空闲线程，若无可回收，则新建线程
newFixedThreadPool      | 创建一个定长线程池，可控制线程最大并发数，超出的线程会在队列中等待
newScheduledThreadPool  | 创建一个定长线程池，支持定时及周期性任务执行
newSingleThreadExecutor | 创建一个单线程化的线程池，它只会用唯一的工作线程来执行任务，保证所有任务按照指定顺序(FIFO, LIFO, 优先级)执行



## RandomAccessFile
如果我们只希望访问文件的部分内容，而不是把文件从头读到尾，使用RandomAccessFile将会带来更简洁的代码以及更好的性能

> getFilePointer()	返回文件记录指针的当前位置
> seek(long pos)	将文件记录指针定位到pos的位置


