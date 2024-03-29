# Drown_Recognition

![](https://github.com/chia-shein/Drown_GIF/blob/main/%E5%81%B4%E8%BA%AB%2000_00_00-00_00_30.gif)
![](https://github.com/chia-shein/Drown_GIF/blob/main/%E6%AD%A3%E9%9D%A2%2000_00_00-00_00_30.gif)
# 1. Prepare
Make sure clone all the file inside this github page.\
Some importance data、model、video put inside the [GoogleDrive](https://drive.google.com/drive/folders/1LpkQqHllmBfhozYpiUWEP-tihkzgzDVC?usp=sharing).\
Put all the files inside the same path of the directories.
## 1.1 Check the environment
**Devices**:
1. Ubuntu 16.04 LTS
2. Memory: 15.6 GiB
3. Processor: Intel® Core™ i5-9400F CPU @ 2.90GHz × 6
4. Graphics : GeForce RTX 2080/PCIe/SSE2
5. Os Type: 64-bit

**Dependency**:
1. Cuda compilation tools, release 10.0, V10.0.130
2. Cudnn : 7.4.2
3. Python : 3.6.12
4. tensorflow-gpu: 1.15.0 
5. keras : 2.3.1

Check Cuda Version:
```bash
nvcc -V
```
Check Cuda Version:
```bash
cat /usr/local/cuda/include/cudnn.h | grep CUDNN_MAJOR -A 2
or
cat /usr/include/cudnn.h | grep CUDNN_MAJOR -A 2
```
## 1.2 Create new environment
Make sure already install Anaconda.

**if not:**

1. Download the {  }.sh file. [here](https://www.anaconda.com/products/individual)
2. Install Anaconda: 
```bash
bash ./{filename.sh}
```
**Completed install Anacconda:**

1. Create new environment and activate:
```bash
conda create -n {env_name} python=3.6.12
conda activate {env_name}
```

## 1.3 Install Tensorflow GPU version
1. Install tensorflow-gpu 1.15.0 version(make sure your tensorflow-gpu version is fit to your cuda version)
```bash
pip3 install tensorflow-gpu==1.15.0
```
2. Check if your tensorflow-gpu completed install or not.
```
python
import tensorflow as tf
tf.__version__
```
>1.15.0

# 2. Install OpenPose
## 2.1 Install dependencies(Tensorflow version)
```bash
cd src/depends/tf-pose-estimation
pip3 install -r requirements.txt
```
## 2.2 Download Pretrained models(MobileNet-Thin models)
MobileNet-Thin models has been inside, see folder:
```
src/depends/tf-pose-estimation/models/graph
cmu  mobilenet_thin  mobilenet_v2_large  mobilenet_v2_small
```
Choose to download(CMU models)

Original Version more accuracy but large and long execution time:
```
cd models/graph/cmu
bash download.sh
```
## 2.3 Install Libraries
```
cd ../../../
pip3 install jupyter tqdm
pip3 install keras==2.3.1
sudo apt install swig
```

## 2.4 Compile c++ library
```bash
pip3 install "git+https://github.com/philferriere/cocoapi.git#egg=pycocotools&subdirectory=PythonAPI"
cd src/depends/tf-pose-estimation/tf_pose/pafprocess
swig -python -c++ pafprocess.i && python3 setup.py build_ext --inplace
```
## 2.5 final install some library
```
cd ../../../../../
pip3 install -r requirements.txt
```
## 2.6 Final Check~

Test on video:
```
python src/s5_test.py \
    --model_path model/trained_classifier.pickle \
    --data_type video \
    --data_path data_test/exercise.avi \
    --output_folder output
```
**if error occurred!**
```
cd src/depends/tf-pose-estimation
python setup.py install
```
>Then try Final check again.

# 3. NOW TRAINING!

# Reference:
1. [Chenge Yang, Zhicheng Yu, Feiyu Chen, "Human Pose Estimation Benchmarking and Action Recognition," Deep Learning Project, Winter 2019, Northwestern University, 26-Oct-2019.](https://github.com/ChengeYang/Human-Pose-Estimation-Benchmarking-and-Action-Recognition)
2. [Feiyu Chen, "Human-Pose-Estimation-Benchmarking-and-Action-Recognition,"Deep Learning Project, Winter 2019, Northwestern University, 26-Oct-2019.](https://github.com/felixchenfy/Realtime-Action-Recognition)
3. [jiajunhua, "ildoonet-tf-pose-estimation," 10-Apr-2019](https://github.com/jiajunhua/ildoonet-tf-pose-estimation)
4. [philferriere ,"cocoapi,"25-Oct-2018](https://github.com/philferriere/cocoapi)
5. [橘白卯咪,"欸你在幹嘛?跟一眼瞬間就懂你的行為辨識技術初次見面," 01-Sep-2020](https://ithelp.ithome.com.tw/users/20129150/ironman/2969)
6. [Zhe Cao, Gines Hidalgo, Tomas Simon, Shih-En Wei, Yaser Sheikh,"OpenPose: Realtime Multi-Person 2D Pose Estimation using Part Affinity Fields,"Computer Vision and Pattern Recognition,18-Dec-2018](https://arxiv.org/abs/1812.08008)
