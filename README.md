# CarrotGAN
### All U Can Eat 智助餐
#### For 2020 CHT IoT competition

## About
紀錄使用CycleGAN-pix2pix的過程，用以生成有紅蘿蔔照片，意即有無紅蘿蔔菜色的風格轉換。

Record the process that I use CycleGAN-pix2pix to transfer the photo without Carrot to with carrot's one.

## Date
* 2020/11/25 Upload ver.1

TBC....

## Prerequisites

( Lab Docker ) cu10.1-dnn7.6-gpu-pytorch-cv-19.12

dir clone /home/ubuntu/Desktop/tso (PC) and /workspace/tso (Docker)

## Refrence

* [CycleGAN and pix2pix in PyTorch](https://github.com/junyanz/pytorch-CycleGAN-and-pix2pix)

## Train / Test CarrotGAN
- Prepare training dataset
```bash
#Copy PC data2docker
#trainA have without Carrot data, trainB have with Carrot data
#testA have Without Carrot data that u want to change it to with Carrot, testB is reverse
#meals have (testA,testB,trainA,trainB) dir
docker cp /home/ubuntu/Desktop/meals /workspace/pytorch-CycleGAN-and-pix2pix/datasets/meals
```
- Train a model
```bash
#dataroot : path of training and testing data meals=(testA,testB,trainA,trainB)
#name : your own model name
#Under /workspace/pytorch-CycleGAN-and-pix2pix
python train.py --dataroot ./datasets/meals --name meals_cyclegan --model cycle_gan
```
- Test the model
  - Without Carrot 2 with Carrot
  ```bash
  #Copy PC testing data2docker (move dir testA to docker)
  #testA have the photo that Without carrot and U want to test
  docker cp /home/ubuntu/Desktop/meals/testA /workspace/pytorch-CycleGAN-and-pix2pix/datasets/meals/testA
  ```
  - The test results will be saved to a html file here: `./results/meals_cyclegan/latest_test/index.html`.
- Copy results to PC
  ```bash
  #docker dir =/workspace/tso is clone to PC dir
  cp -r test_latest /workspace/tso
  ```
