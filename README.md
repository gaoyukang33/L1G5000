# L1G5000 #
## 配置环境 ##     
安装必要的运行环境         
### 步骤一：创建虚拟环境 ###
首先使用`conda create -n xtuner-env python=3.10 -y`和`conda activate xtuner-env`            
安装一个Python-3.10 的虚拟环境       
### 步骤二：配置包 ###
使用之前我们学过的`requirements.txt`文档安装必要的包，安装过程较长                
安装后我们使用`xtuner list-cfg`来验证是否安装成功，输出如下结果：          
![image](https://github.com/gaoyukang33/L1G5000/blob/main/IMG/8d8c083738e67eeef8ab749053eef92.png)            
## 训练启动 ##   
### 步骤一：修改提供的数据 ###         
修改`change_script.py``--new_text`中的`default="嘟嘟"` 为嘟嘟      
![image](https://github.com/gaoyukang33/L1G5000/blob/main/IMG/3e78820fbf4764639e9905f9b40b0b5.png)                
然后使用`cat assistant_Tuner_change.jsonl | head -n 3`查看修改后的数据，输出如下，可以看到输出文本中已经包含'嘟嘟'字样：     
![image](https://github.com/gaoyukang33/L1G5000/blob/main/IMG/492e6efefa34e18d780646ec7ad2d81.png)      
### 步骤二：修改Config ###       
按照文档的引导，修改部分Config中的语句           
## 训微调启动 ##      
使用如下语句启动微调         
`xtuner train ./config/internlm2_5_chat_7b_qlora_alpaca_e3_copy.py --deepspeed deepspeed_zero2 --work-dir ./work_dirs/assistTuner`     
经过漫长的微调，输出以下结果，说明此时训练已经完成：          
![image](https://github.com/gaoyukang33/L1G5000/blob/main/IMG/723abf61a082e66cfd40d9a0ace3c2d.png)         
## 模型合并 ##      
使用文档的命令，得到合并后的目录结构如下：      
![image](https://github.com/gaoyukang33/L1G5000/blob/main/IMG/eedd8e55433c841ca5e813492ce3d0e.png)      
## 模型 WebUI 对话 ##      
首先修改脚本文件第18行的路径为：`model_name_or_path = "/root/finetune/work_dirs/assistTuner/merged"`      
然后直接启动应用`streamlit run /root/Tutorial/tools/L1_XTuner_code/xtuner_streamlit_demo.py`          
访问网站前记得要进行端口映射      
![image](https://github.com/gaoyukang33/L1G5000/blob/main/IMG/a283598984775b54d8b7f1718ae161b.png)        
![image](https://github.com/gaoyukang33/L1G5000/blob/main/IMG/51cb24feafb55a2e582e730cb6a2a42.png)      

