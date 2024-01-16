---
{"dg-publish":true,"permalink":"/OperatingSystem/Linux/ssh/","noteIcon":"3"}
---

#ssh
ssh connection remote operations
environment variables
remote ssh nohup no default output file

bashrc disable ps1 

如果想在集群中的多个节点分发任务或者修改文件，一个一个登录操作比较麻烦，可以通过在已和其他子节点免密的主节点通过ssh向集群中的子节点进行分发任务来减少工作量。
ssh连接执行命令与正常ssh交互式登录是存在差别的，系统一般将ssh执行命令视作风险比较高的操作，一些环境变量是缺失的，比如~/.bashrc第一行就判断当前会话是否是交互式登录，如果不是的话直接return
为了将我们任务分发时必要的环境变量保存，我们可以打开/etc/ssh/sshd_config文件中的PermitUserEnvironment选项，然后restart ssh
将每个子节点的必要的环境变量导入到~/.ssh/environment文件中，这样主节点命令行方式对于子节点的ssh会话都会读取该文件中的环境变量
```bash
PermitUserEnvironment yes
service ssh restart
env >> ~/.ssh/environment

```
多节点交互式登录设置的环境变量

```bash
for i in {1..10}
do
  ssh node${i} "tee -a ~/.bashrc <<< 'export PATH=/usr/local/python3.8.12/bin:\$PATH'"
done
```

远程ssh连接进行多任务分发

```bash
#这里主节点进行任务分发时将子节点的train.sh的stdout输出到/dev/null，不输出到主节点的屏幕中，注意这里的train.sh最好本身就使用tee将输出导入到本地日志文件中
# 每次ssh命令之后会卡住，需要ctrl c 10次，注意不能ctrl c掉当前for循环命令，最后ctrl z加上bg来使得命令后台运行，最后使用disown来将for循环的后台任务与当前会话分离，防止ssh中断导致任务中断
for i in {1..10}
do
  nohup ssh node{i} "nohup bash train.sh > nohup.out  &" > node${i}.log &
done

```

