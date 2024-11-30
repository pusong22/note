# c# 语言特性
## ref/in/out
1. 它们都能将参数按照引用方式传递
### in 与 struct结合使用，需要加上readonly struct，否则会创建大量的备份副本


## struct是值类型，在堆栈上保存，但是当struct申明的类型作为类中的变量时，它会以引用形式存储。