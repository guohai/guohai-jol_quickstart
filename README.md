
Hello Jol!

Only works on HotSpot/OpenJDK VMs.

Quotes from VM specifictions
> For example, the memory layout of run-time data areas, the garbage-collection algorithm used, and any internal optimization of the Java Virtual Machine instructions (for example, translating them into machine code) are left to the discretion of the implementor.

[JOL](https://github.com/openjdk/jol) (Java Object Layout) is the tiny toolbox to analyze object layout schemes in JVMs.

`./gradlew clean check`

`./gradlew clean test`

`./gradlew clean run`

```bash
guohai@kleokooe:~/work/jol_quickstart$ ./gradlew clean run
WARNING: JNI local refs: 33, exceeds capacity: 32
        at com.sun.management.internal.DiagnosticCommandImpl.getDiagnosticCommandInfo(jdk.management@11.0.2/Native Method)
        at com.sun.management.internal.DiagnosticCommandImpl.getMBeanInfo(jdk.management@11.0.2/DiagnosticCommandImpl.java:196)
        at com.sun.jmx.interceptor.DefaultMBeanServerInterceptor.getNewMBeanClassName(java.management@11.0.2/DefaultMBeanServerInterceptor.java:329)
        at com.sun.jmx.interceptor.DefaultMBeanServerInterceptor.registerMBean(java.management@11.0.2/DefaultMBeanServerInterceptor.java:315)
        at com.sun.jmx.mbeanserver.JmxMBeanServer.registerMBean(java.management@11.0.2/JmxMBeanServer.java:522)
        at java.lang.management.ManagementFactory.lambda$addMXBean$7(java.management@11.0.2/ManagementFactory.java:901)
        at java.lang.management.ManagementFactory$$Lambda$47/0x0000000800127440.run(java.management@11.0.2/Unknown Source)
        at java.security.AccessController.doPrivileged(java.base@11.0.2/Native Method)
        at java.lang.management.ManagementFactory.addMXBean(java.management@11.0.2/ManagementFactory.java:891)
        at java.lang.management.ManagementFactory.lambda$getPlatformMBeanServer$1(java.management@11.0.2/ManagementFactory.java:488)
        at java.lang.management.ManagementFactory$$Lambda$46/0x0000000800127040.accept(java.management@11.0.2/Unknown Source)
        at java.util.stream.ForEachOps$ForEachOp$OfRef.accept(java.base@11.0.2/ForEachOps.java:183)
        at java.util.Collections$2.tryAdvance(java.base@11.0.2/Collections.java:4745)
        at java.util.Collections$2.forEachRemaining(java.base@11.0.2/Collections.java:4753)
        at java.util.stream.ReferencePipeline$Head.forEach(java.base@11.0.2/ReferencePipeline.java:658)
        at java.util.stream.ReferencePipeline$7$1.accept(java.base@11.0.2/ReferencePipeline.java:274)
        at java.util.stream.ReferencePipeline$2$1.accept(java.base@11.0.2/ReferencePipeline.java:177)
        at java.util.HashMap$ValueSpliterator.forEachRemaining(java.base@11.0.2/HashMap.java:1675)
        at java.util.stream.AbstractPipeline.copyInto(java.base@11.0.2/AbstractPipeline.java:484)
        at java.util.stream.AbstractPipeline.wrapAndCopyInto(java.base@11.0.2/AbstractPipeline.java:474)
        at java.util.stream.ForEachOps$ForEachOp.evaluateSequential(java.base@11.0.2/ForEachOps.java:150)
        at java.util.stream.ForEachOps$ForEachOp$OfRef.evaluateSequential(java.base@11.0.2/ForEachOps.java:173)
        at java.util.stream.AbstractPipeline.evaluate(java.base@11.0.2/AbstractPipeline.java:234)
        at java.util.stream.ReferencePipeline.forEach(java.base@11.0.2/ReferencePipeline.java:497)
        at java.lang.management.ManagementFactory.getPlatformMBeanServer(java.management@11.0.2/ManagementFactory.java:488)
        - locked <0x0000000751ac1ef8> (a java.lang.Class for java.lang.management.ManagementFactory)
        at org.openjdk.jol.vm.VMOptions.getString(VMOptions.java:37)
        at org.openjdk.jol.vm.VMOptions.pollCompressedOops(VMOptions.java:45)
        at org.openjdk.jol.vm.HotspotUnsafe.<init>(HotspotUnsafe.java:133)
        at org.openjdk.jol.vm.VM.current(VM.java:81)
        at org.openjdk.jol.layouters.CurrentLayouter.layout(CurrentLayouter.java:52)
        at org.openjdk.jol.info.ClassLayout.parseInstance(ClassLayout.java:102)
        at org.openjdk.jol.info.ClassLayout.parseInstance(ClassLayout.java:85)
        at jol.quickstart.App.main(App.java:32)

jol.quickstart.App$Car object internals:
OFF  SZ               TYPE DESCRIPTION               VALUE
  0   8                    (object header: mark)     0x0000000000000005 (biasable; age: 0)
  8   4                    (object header: class)    0x00060250
 12   4                int Car.id                    3
 16   8             double Car.price                 133.9
 24   2               char Car.level                 A
 26   2                    (alignment/padding gap)
 28   4   java.lang.String Car.type                  (object)
Instance size: 32 bytes
Space losses: 2 bytes internal + 0 bytes external = 2 bytes total

[I object internals:
OFF  SZ   TYPE DESCRIPTION               VALUE
  0   8        (object header: mark)     0x0000000000000001 (non-biasable; age: 0)
  8   4        (object header: class)    0x00000c10
 12   4        (array length)            3
 12   4        (alignment/padding gap)
 16  12    int [I.<elements>             N/A
 28   4        (object alignment gap)
Instance size: 32 bytes
Space losses: 4 bytes internal + 4 bytes external = 8 bytes total
```

Reference:

>[Building Java Applications Sample](https://docs.gradle.org/current/samples/sample_building_java_applications.html)


>[Chapter 2. The Structure of the Java Virtual Machine](https://docs.oracle.com/javase/specs/jvms/se14/html/jvms-2.html)

