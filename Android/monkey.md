# monkey

Monkey 测试出现错误后，一般的分析步骤
看Monkey的日志 (为了进一步分析问题的来源，可以找到Log中出现问题处的前一次Switch，随后根据Log主要是查看相关的Activity)
1、程序无响应的问题：在日志中搜索 “ANR”

可能原因：当前有耗时操作在UI线程指定，导致卡UI了；在5秒内没有响应输入的事件（例如，按键按下，屏幕触摸）;BroadcastReceiver在10秒内没有执行完毕

2、崩溃问题：在日志中搜索 “Exception” (如果出现空指针， NullPointerException) 肯定是有bug
3、搜索"crash" 、"error"

Monkey 执行中断， 在log最后也能看到当前执行次数；若以上步骤还不能定位问题，可以使用之前执行的monkey命令再执行一遍，注意seed值要一样
