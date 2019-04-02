# homework3-GAN-Dissection

## Generate images with GANPaint

## Dissect any GAN model and analyze what you find

## Compare with other method
這裡就inpainting的部分，與[Globally and Locally Consistent Image Completion](http://iizuka.cs.tsukuba.ac.jp/projects/completion/en/)比較。

### Method
![](http://iizuka.cs.tsukuba.ac.jp/projects/completion/images/model_v2.png)
如上圖所示，這個方法使用了三個networks，其中completion network是用來產生完整的圖片的，global和local discriminator則是幫助訓練。global discriminator能看到整張圖片，幫助達成整個圖片的連貫，local discriminator則只會看到一部份的input圖片，讓局部區域能夠一致。在訓練過程中，除了來自兩個discriminators的GAN loss以外，還加上了和原圖比較的MSE loss，讓model更加穩定。最後，對輸出的圖片有使用簡單的後處理，調整補上部分的顏色符合其四周的顏色。
