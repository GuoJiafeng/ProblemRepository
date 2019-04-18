原文 <https://blog.csdn.net/yjc_1111/article/details/78819938>





一、commons-io方法

1、使用Commons-io的monitor下的相关类可以处理对文件进行监控，它采用的是观察者模式来实现的

（1）可以监控文件夹的创建、删除和修改
（2）可以监控文件的创建、删除和修改
（3）采用的是观察者模式来实现的
（4）采用线程去定时去刷新检测文件的变化情况

2、引入commons-io包，需要2.0以上。





~~~


<!-- https://mvnrepository.com/artifact/commons-io/commons-io -->
<dependency>
    <groupId>commons-io</groupId>
    <artifactId>commons-io</artifactId>
    <version>2.6</version>
</dependency>
~~~





3、编写继承FileAlterationListenerAdaptor的类FileListener。



~~~
import java.io.File;

import org.apache.commons.io.monitor.FileAlterationListenerAdaptor;
import org.apache.commons.io.monitor.FileAlterationObserver;
import org.apache.log4j.Logger;

/**

- 文件变化监听器
  *

- 在Apache的Commons-IO中有关于文件的监控功能的代码. 文件监控的原理如下：

- 由文件监控类FileAlterationMonitor中的线程不停的扫描文件观察器FileAlterationObserver，

- 如果有文件的变化，则根据相关的文件比较器，判断文件时新增，还是删除，还是更改。（默认为1000毫秒执行一次扫描）
  *
   *
   */
  public class FileListener extends FileAlterationListenerAdaptor {
  private Logger log = Logger.getLogger(FileListener.class);
  /**

  - 文件创建执行
    */
    public void onFileCreate(File file) {
    log.info("[新建]:" + file.getAbsolutePath());
    }

  /**

  - 文件创建修改
    */
    public void onFileChange(File file) {
    log.info("[修改]:" + file.getAbsolutePath());
    }

  /**

  - 文件删除
    */
    public void onFileDelete(File file) {
    log.info("[删除]:" + file.getAbsolutePath());
    }

  /**

  - 目录创建
    */
    public void onDirectoryCreate(File directory) {
    log.info("[新建]:" + directory.getAbsolutePath());
    }

  /**

  - 目录修改
    */
    public void onDirectoryChange(File directory) {
    log.info("[修改]:" + directory.getAbsolutePath());
    }

  /**

  - 目录删除
    */
    public void onDirectoryDelete(File directory) {
    log.info("[删除]:" + directory.getAbsolutePath());
    }

  public void onStart(FileAlterationObserver observer) {
      // TODO Auto-generated method stub
      super.onStart(observer);
  }

  public void onStop(FileAlterationObserver observer) {
      // TODO Auto-generated method stub
      super.onStop(observer);
  }

}

4、实现main方法

public static void main(String[] args) throws Exception{
        // 监控目录
        String rootDir = "D:\\apache-tomcat-7.0.78";
        // 轮询间隔 5 秒
        long interval = TimeUnit.SECONDS.toMillis(1);
        // 创建过滤器
        IOFileFilter directories = FileFilterUtils.and(
                FileFilterUtils.directoryFileFilter(),
                HiddenFileFilter.VISIBLE);
        IOFileFilter files       = FileFilterUtils.and(
                FileFilterUtils.fileFileFilter(),
                FileFilterUtils.suffixFileFilter(".txt"));
        IOFileFilter filter = FileFilterUtils.or(directories, files);
        // 使用过滤器
        FileAlterationObserver observer = new FileAlterationObserver(new File(rootDir), filter);
        //不使用过滤器
        //FileAlterationObserver observer = new FileAlterationObserver(new File(rootDir));
        observer.addListener(new FileListener());
        //创建文件变化监听器
        FileAlterationMonitor monitor = new FileAlterationMonitor(interval, observer);
        // 开始监控
        monitor.start();
    }
~~~





二、使用JDK7提供的WatchService

public static void main(String[] a) {

        final Path path = Paths.get("D:\\apache-tomcat-7.0.78");
    
        try (WatchService watchService = FileSystems.getDefault().newWatchService()) {
            //给path路径加上文件观察服务
            path.register(watchService, StandardWatchEventKinds.ENTRY_CREATE,
                    StandardWatchEventKinds.ENTRY_MODIFY,
                    StandardWatchEventKinds.ENTRY_DELETE);
            while (true) {
                final WatchKey key = watchService.take();
    
                for (WatchEvent<?> watchEvent : key.pollEvents()) {
    
                    final WatchEvent.Kind<?> kind = watchEvent.kind();
    
                    if (kind == StandardWatchEventKinds.OVERFLOW) {
                        continue;
                    }
                    //创建事件
                    if (kind == StandardWatchEventKinds.ENTRY_CREATE) {
                        System.out.println("[新建]");
                    }
                    //修改事件
                    if (kind == StandardWatchEventKinds.ENTRY_MODIFY) {
                        System.out.println("修改]");
                    }
                    //删除事件
                    if (kind == StandardWatchEventKinds.ENTRY_DELETE) {
                        System.out.println("[删除]");
                    }
                    // get the filename for the event
                    final WatchEvent<Path> watchEventPath = (WatchEvent<Path>) watchEvent;
                    final Path filename = watchEventPath.context();
                    // print it out
                    System.out.println(kind + " -> " + filename);
    
                }
                boolean valid = key.reset();
                if (!valid) {
                    break;
                }
            }
    
        } catch (IOException | InterruptedException ex) {
            System.err.println(ex);
        }
    
    }

三、以上方法都可以实现对相应文件夹得文件监控，但是在使用jdk7提供的API时，会出现些许问题。

（1）当文件修改时，会被调用两次，即输出两个相同的修改。
（2）不能对其子文件夹进行监控，只能提示目录被修改。
（3）无法对文件类型进行过滤。