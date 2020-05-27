# Java虚拟机（JVM）面试题大集合

- 1、Java内存区域

- - 说一下 JVM 的主要组成部分及其作用？
  - 说一下 JVM 运行时数据区
  - 深拷贝和浅拷贝
  - 说一下堆栈的区别？
  - 队列和栈是什么？有什么区别？

- 2、HotSpot虚拟机对象探秘

- - 对象的创建

  - 为对象分配内存

  - 处理并发安全问题

  - 对象的访问定位

  - - 句柄访问
    - 直接指针

- 3、内存溢出异常

- - Java会存在内存泄漏吗？请简单描述

- 4、GC垃圾收集器

- - 简述Java垃圾回收机制

  - GC是什么？为什么要GC

  - 垃圾回收的优点和原理。并考虑2种回收机制

  - 垃圾回收器的基本原理是什么？垃圾回收器可以马上回收内存吗？有什么办法主动通知虚拟机进行垃圾回收？

  - Java 中都有哪些引用类型？

  - 怎么判断对象是否可以被回收？

  - 在Java中，对象什么时候可以被垃圾回收

  - JVM中的永久代中会发生垃圾回收吗

  - 说一下 JVM 有哪些垃圾回收算法？

  - - 标记-清除算法
    - 复制算法
    - 标记-整理算法
    - 分代收集算法

  - 说一下 JVM 有哪些垃圾回收器？

  - 详细介绍一下 CMS 垃圾回收器？

  - 新生代垃圾回收器和老年代垃圾回收器都有哪些？有什么区别？

  - 简述分代垃圾回收器是怎么工作的？

- 5、内存分配策略

- - 简述java内存分配与回收策率以及Minor GC和Major GC

  - - 对象优先在 Eden 区分配
    - 大对象直接进入老年代
    - 长期存活对象将进入老年代

- 6、虚拟机类加载机制

- - 简述java类加载机制?
  - 描述一下JVM加载Class文件的原理机制
  - 什么是类加载器，类加载器有哪些?
  - 说一下类装载的执行过程？
  - 什么是双亲委派模型？

- 7、JVM调优

- - 说一下 JVM 调优的工具？
  - 常用的 JVM 调优的参数都有哪些？

Java内存区域

### **说一下 JVM 的主要组成部分及其作用？**

![](https://raw.githubusercontent.com/sanzhixiong19860117/DayInterViewQuestions/master/2020-5-27/640.webp)

JVM包含两个子系统和两个组件，两个子系统为Class loader(类装载)、Execution engine(执行引擎)；两个组件为Runtime data area(运行时数据区)、Native Interface(本地接口)。

- Class loader(类装载)：根据给定的全限定名类名(如：java.lang.Object)来装载class文件到Runtime data area中的method area。
- Execution engine（执行引擎）：执行classes中的指令。
- Native Interface(本地接口)：与native libraries交互，是其它编程语言交互的接口。
- Runtime data area(运行时数据区域)：这就是我们常说的JVM的内存。

**作用** ：首先通过编译器把 Java 代码转换成字节码，类加载器（ClassLoader）再把字节码加载到内存中，将其放在运行时数据区（Runtime data area）的方法区内，而字节码文件只是 JVM 的一套指令集规范，并不能直接交给底层操作系统去执行，因此需要特定的命令解析器执行引擎（Execution Engine），将字节码翻译成底层系统指令，再交由 CPU 去执行，而这个过程中需要调用其他语言的本地库接口（Native Interface）来实现整个程序的功能。

**下面是Java程序运行机制详细说明**

Java程序运行机制步骤

- 首先利用IDE集成开发工具编写Java源代码，源文件的后缀为.java；
- 再利用编译器(javac命令)将源代码编译成字节码文件，字节码文件的后缀名为.class；
- 运行字节码的工作是由解释器(java命令)来完成的。

![](https://raw.githubusercontent.com/sanzhixiong19860117/DayInterViewQuestions/master/2020-5-27/641.webp)



