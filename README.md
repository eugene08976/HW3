# homework3-GAN-Dissection

## Generate images with GANPaint
* 
* 

![](https://i.imgur.com/UX1BGAS.jpg)
![](https://i.imgur.com/zUgg0dh.png)
![](https://i.imgur.com/6Tj57A7.png)
![](https://i.imgur.com/7cgeqAj.png)
![](https://i.imgur.com/04Hozyq.png)
![](https://i.imgur.com/6qZoC9Y.png)
> It is impossible to generate grass in the sky and **the GAN know that**.

![](https://i.imgur.com/EBBkvIE.jpg)

* 目前來看，除了 Remove bricks 主觀看起來效果不怎麼好，其餘的都補圖的還算正常跟合理


---
## Dissect any GAN model and analyze what you find
### 1. layer1
#### living room：
![](https://imgur.com/3OTnaOq.png)
#### bed room：
![](https://imgur.com/EQCiuFc.png)
#### 觀察：
* 客廳

    - 圈選出來的物件都很局部細微，看不太出來特別想學什麼類型的物件
    - 

* 臥室

    - 圈選的物件以局部的床、枕頭居多
    - 效果比 layer1 的客廳略好

### 2. layer4
#### living room：
![](https://imgur.com/yaoQO35.png)

#### bed room：
![](https://imgur.com/6Wj5QfG.png)
#### 觀察：
* 客廳

    - 有試圖縮小圈選範圍，但選取的效果不是到很好

* 臥室

    - 圈選的物件以床、枕頭、櫃子、窗戶居多
    - 物件辨識的框種類繁多
    - 效果比 layer1 好

### 3. layer7
#### living room：
![](https://imgur.com/pK07WML.png)
#### bed room：
![](https://imgur.com/G9R0RB6.png)
#### 觀察：
* 客廳

    - 能圈選出較細緻的家具

* 臥室

    - 圈選的物件仍以床、枕頭居多
    - 但框出來的區域沒有很完整，反而都是大物件局部的區域
    - 效果感覺比 layer4 的略差，但比 layer1 略好 


---
## Compare with other method
這裡就inpainting的部分，與[Globally and Locally Consistent Image Completion](http://iizuka.cs.tsukuba.ac.jp/projects/completion/en/)比較。

### Method
![](http://iizuka.cs.tsukuba.ac.jp/projects/completion/images/model_v2.png)
如上圖所示，這個方法使用了三個networks，其中completion network是用來產生完整的圖片的，global和local discriminator則是幫助訓練。global discriminator能看到整張圖片，幫助達成整個圖片的連貫，local discriminator則只會看到一部份的input圖片，讓局部區域能夠一致。在訓練過程中，除了來自兩個discriminators的GAN loss以外，還加上了和原圖比較的MSE loss，讓model更加穩定。最後，對輸出的圖片有使用簡單的後處理，調整補上部分的顏色符合其四周的顏色。
