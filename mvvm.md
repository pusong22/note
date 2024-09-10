# ICommand
接口
```c#
bool CanExecute(object parameter);
void Execute(object parameter);
event EventHandler CanExecuteChanged;
```
重点是CanExecuteChanged事件的处理方式，像下面写或者直接不管两种情况会产生不一样的效果
```c#
public event EventHandler CanExecuteChanged
{
    add
    {
        CommandManager.RequerySuggested += value;
        this.CanExecuteChangedInternal += value;
    }

    remove
    {
        CommandManager.RequerySuggested -= value;
        this.CanExecuteChangedInternal -= value;
    }
}
```
上面的代码会自动触发```CanExecute```方法来设置状态。不加这段代码如果想要设置状态需要用到```CommandManager.InvalidateRequerySuggested()```手动触发。（以上用在需要时刻刷新状态的场景）
