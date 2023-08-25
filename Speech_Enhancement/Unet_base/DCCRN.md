# DCCRN: Deep Complex Convolution Recurrent Network for Phase-Aware Speech Enhancement

## 期刊/会议
 Interspeech 2020

## Abs&Intro
1. 提出了复数卷积以及复数lstm，结合了crn和dcunet的优点，利用了复数乘法的特性
2. 参数量小、效率高

## Method
1. Framework
![img.png](../Img/DCCRN/DCCRM_framework.png)

2. 复数卷积
![img.png](../Img/DCCRN/img.png)  
复数卷积的W定义为：W_r+W_i*j ,其中 W_r 和 W_i 分别是实部卷积和虚部卷积的W  
模型的输入 X = X_r +j*X_i  
模型的输出  
![img_1.png](../Img/DCCRN/img_1.png)  

3. 复数LSTM
![img_2.png](../Img/DCCRN/img_2.png)

4. 训练目标  
S 干净语音的实虚部， Y 带噪语音的实虚部  
![img_3.png](../Img/DCCRN/img_3.png)  
![img_4.png](../Img/DCCRN/img_4.png)    
提出了三种预测方式（mask乘在不同地方）  
![img_5.png](../Img/DCCRN/img_5.png)

6. Loss  
MES  
![img_6.png](../Img/DCCRN/img_6.png)


