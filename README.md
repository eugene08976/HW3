# homework3-GAN-Dissection

## Generate images with GANPaint
> Draw tree
![](https://i.imgur.com/UX1BGAS.jpg)
* 可以把樹畫在天空，不像草可以排除天空的可能
> Draw grass in the sky
![](https://i.imgur.com/zUgg0dh.png)
* 不能把草畫在天空，但被畫的範圍有點綠綠的
> Draw grass
![](https://i.imgur.com/6Tj57A7.png)
> Draw brick
![](https://i.imgur.com/7cgeqAj.png)
> Remove dome
![](https://i.imgur.com/04Hozyq.png)
> Remove door
![](https://i.imgur.com/6qZoC9Y.png)
＊ 主觀來看，除了generate tree的部分有些情況會有不合理的情況產生，其他generate跟remove的效果都不錯
---
## Dissect any GAN model and analyze what you find
### 1. layer1
#### living room：
![](https://i.imgur.com/raticD4.png)
#### bed room：
![](https://i.imgur.com/GE2Ywht.png)
#### Observation：
* 臥室效果比客廳好，可能是因為臥室圈選的物件以床、枕頭以及燈為主，而客廳都是圈選範圍太小，學習效果較差
### 2. layer4
#### living room：
![](https://i.imgur.com/k4bsjja.png)
#### bed room：
![](https://i.imgur.com/5kxuGun.png)
#### Observation：
* 客廳的圈選範圍還是太小，雖比layer1大，但仍然無法學到途中完整的物件，臥室除了layer1有圈選到的物件以外多了窗戶與衣櫃，辨識的物件更多元
### 3. layer7
#### living room：
![](https://i.imgur.com/B5oBR2O.png)
#### bed room：
![](https://i.imgur.com/SHsjrer.png)
#### Observation：
* 客廳能圈選出圖中較小較細節的物件，臥室圈選的以大物件為主，雖然是layer7但感覺效果不是最好的
---
## Compare with other method
這裡就inpainting的部分，與[Globally and Locally Consistent Image Completion](http://iizuka.cs.tsukuba.ac.jp/projects/completion/en/)比較。

### Method
![](http://iizuka.cs.tsukuba.ac.jp/projects/completion/images/model_v2.png)
如上圖所示，這個方法使用了三個networks，其中completion network是用來產生完整的圖片的，global和local discriminator則是幫助訓練。global discriminator能看到整張圖片，幫助達成整個圖片的連貫，local discriminator則只會看到一部份的input圖片，讓局部區域能夠一致。在訓練過程中，除了來自兩個discriminators的GAN loss以外，還加上了和原圖比較的MSE loss，讓model更加穩定。最後，對輸出的圖片有使用簡單的後處理，調整補上部分的顏色符合其四周的顏色。
