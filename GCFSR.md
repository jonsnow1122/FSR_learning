# GCFSR——一种细节可控的高倍人脸超分方法    
![image name](https://i.postimg.cc/qMR4FsNS/v2-c27c6a50a1f79d38dab3416f01a98c12-1440w.jpg)  
## 背景  
### GAN（生成对抗网络）  
包含生成模型和判别模型，通过不断重复训练两种模型，最终获得效果最好的两种模型
[GAN learning web](https://easyai.tech/ai-definition/gan/)  
## GCRSR  
### 特点
1.**无需人脸先验和GAN先验**，实现高保真度、清晰面部细节的face SR；
2.  通过一个放大因子s，可以调整图像的**生成强度**，实现可控的生成细节；
3.  相较于GAN先验方法，更优越的SR效果。

### 网络结构  
![image](https://i.postimg.cc/PJpg57tp/image.png)    
#### encoder network  
是一个以2位步长的CNN  
输入为bicubic降采样图片  
#### generator network  
style modulation:利用顶层编码的feature map和latent code生成真实的面部细节  
feature modulation：控制上采样系数s
### related work  
用priors还是不用priors  
#### GAN-prior-based Methods  
1.GLEAN
2.GFP-GAN
3.GPEN  
### 实验  
损失函数：L1, perceptual and adversarial losses，给三者赋予不同的权重  

train:
FFHQ dataset：70k high-quality 1024 × 1024 face images  
test:  
extract 100 images from CelebA-HQ dataset  
evaluation:  
non-reference perceptual metrics: FID and NIQE   
pixel-wise metrics (PSNR and SSIM) and the perceptual metric (LPIPS )  

#### 实验内容  
1.与已有方法对比：quantitative and qualitative results for 16×, 32×, 64× SR tasks（GLEAN is designed for SR task on single upscaling factor？）
2.测试s带来的影响：取{4, 8, 16, 32, 64}进行测试，再在32周边取了24和48来测试s取值对结果影响的连续性  
3.blind face restoration (BFR) task：与已有算法对比效果最佳  
4.对feature modulation进行分析  
5.只用一种损失函数对（4和8）这种small factor产生最好的结果  
6.style modulation:用眼睛和头发展示细节生成效果
