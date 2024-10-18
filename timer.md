# wpf中常用的定时器
1. System.Windows.Threading.DispatcherTImer  
基于Dispatcher的计时器，在ui线程更新。
2. System.Timers.Timer  
基于线程的计时器，触发Elapsed事件。跨线程更新ui需要调用Dispatcher。
3. System.Threading.Timer  
基于线程池的计时器。
4. System.Windows.Forms.Timer  
基于Windows Forms的计时器，不建议使用。