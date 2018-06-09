# ML-Agent.01_3dball
ml-agent v0.3 win10安装和实践
参考文档
Migrating to ML-Agents v0.3
Getting Started with the 3D Balance Ball Environment
Training ML-Agents
ml-agent v0.2：Win10下环境安装
前言
        近段时间，ml-agent升级到了v0.3版本，做了一些变更，导致之前的文档《ml-agent v0.2：Win10下环境安装》部分内容无法在ml-agent v0.3中使用。最主要的是ppo.ipynb文件移除，导致无法用ppo进行训练。所以这里进行重新整理。

软件安装
推荐的环境
Phython3 64位（ml-agent v0.3不再支持Phython2）
Jupyter notebook
TensorFlow
Visual Studio 2017
Unity3d 2017.1(本文使用)/2018.1
1、克隆ml-agent
        从Github网站上https://github.com/Unity-Technologies/ml-agents克隆（下载）ml-agent，代码，放在任意位置下。(本文放在D:\ml-agent)

2、安装Visual Studio/Unity3d
        安装略过

3、安装Anaconda 64位
        Anaconda内置了Phython3 64位和Jupyter notebook以及其他便利的功能，所以还是选择安装Anaconda简化整个Phython的过程。下载地址https://www.anaconda.com/download/#windows。安装略过（本文安装在F盘）。安装完成后利用Anaconda的Anaconda Navigator创建一个环境(这里环境名为tensorflow)，Phython版本选择3.6。

4、安装ml-agent依赖库
        在开始菜单中打开Anacoda Prompt，在命令行中输入一下命令来激活刚刚创建的环境

activate tensorflow

        输入命令切换到ml-agent所在的目录中python目录的位置。比如ml-agent安装目录为D:\Git\ml-agent，则输入

cd D:\Git\ml-agent\python

        如果你的Anaconda不是安装在ml-agent目录相同的磁盘，那么需要切换到ml-agen所在的磁盘。比如这里Anaconda的安装目录为F盘，ml-agent安装目录为D:\ml-agent，则需要切换到D盘，输入

D:

        然后开始安装Demo所需的环境，输入命令

pip install .

        注意，不要遗漏最后的点号。等待安装完成即可。该命令会安装所有的依赖库，包括tensorflow。此时不用关闭这个窗口。

5、编译Unity程序
        使用Unity2017打开ml-agent下unity-environment文件夹。

        打开Assets\ML-Agents\Examples\3DBall目录下的3DBall场景文件。在场景中选择Ball3DAcademy下的Ball3DBrain物体，将TypeOfBrain修改为External，表示从Tensorflow中获取数据。


        菜单中选择File->Build Setting，添加当前所在场景。（可以勾选Development Build以便查看输出）

        点击PlayerSeting，检查设置

        Resolution and Presentation -> 勾选Run in Background

        Resolution and Presentation -> Display Resolution Dialog设置为disable

        回到Build Setting面板，点击Build，编译到ml-agent的python目录中。名为3dball.exe


6、开始训练
        注意，训练方法和ml-agent v0.2不同。v0.2使用Jupyter notebook运行ppo.ipynb文件。但是v0.3改为使用命令行的方法。

        我们回到Anacoda Prompt，输入以下命令：

python learn.py 3dball --run-id=test --train

        其中

learn.py包含了大量的ml算法，包括ppo。
3dball就是刚刚我们用unity生成的exe文件的名称。
--run-id=test可以不写，只是声明这次训练的id。比如可以用tensorboard来看
--train表示声明执行的是训练模式
       如果这这些命令参数感兴趣，请参考Training ML-Agents

       由于训练的Step为5.0e4(5*10的4次方)，如果用cpu算比较慢，可以暂时修改超参数配置文件trainer_config.yaml，将Ball3DBrain下增加一行max_steps: 2.0e4（注意，由于该文件采用yaml格式，对文件的编码格式和空格要求非常严格，如果异常，将无法进行训练。max前面有4个空格，不是tab。冒号后面有一个空格，整个文件采用UTF8编码）。


        训练结果数据保存在models\test\下

