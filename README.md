# winTask

##windows系统 PHP定时任务方案

因项目部署在windows环境，windows定时任务不灵活（想每个后台任务可以根据不同的执行周期去执行任务）
当然，windows定时任务确实可以做到，但是每个任务都需要人为去启动，自己写了个PHP定时任务执行方案

##思路：
把任务写入文件，放在一个文件夹下，循环去执行这个文件夹下的任务文件，PHP去执行一个入口文件，保障一直循环此文件夹即可
这样如果有新的任务，只要把任务做成任务文件，放到文件夹下，它就可以自动去执行了

##文件结构介绍
*tasks文件夹：存放后缀为“_task”的任务文件，每个任务一个文件
*delTask.php: 增加任务列表 批量删除任务文件
*f_sleeptime.php: 父级守护休息时间，毫秒为单位
*f_switch.php: 判断是否开启父级守护，如果关闭了，则需要人为启动
*index.php: 启动任务主文件
*sleeptime.php: 子级守护休息时间，毫秒为单位
*switch.php: 子级守护开关

#此设计是为了，在SVN同步项目时，做自动切换

#任务文件格式：

*<?php
return array('name'=>'定时统计','url'=>'task\task1','execTime'=>100,'data'=>array(),'del'=>FALSE);
*?>

#字段说明：
*name: 任务名称
*url: 执行的地址，因我使用的CI框架，所有可以把地址 转换成控制器执行命令
*execTime: 每格多少毫秒执行一次次任务
*data: 执行时需要传递的参数
*del: 此任务是否执行一次就删除，如果是TRUE，则执行完一次后，删除此任务，如为FALSE,则一直根据执行时间执行任务



