Tested on Legion PC, ubuntu20
### 安装依赖项：
1. pangolin: <https://github.com/stevenlovegrove/Pangolin>
    git clone --recursive https://github.com/stevenlovegrove/Pangolin.git
    ./scripts/install_prerequisites.sh recommended
    cmake -B build
    cmake --build build
    (ctest)
2. opencv
    v3.4.5 works, v4 not working
    Install OpenCV 3.4.5
    In CMakeLists.txt, "SET("OpenCV_DIR" "/home/abel/Documents/Software/opencv")"
3. Eigen
4. Ceres: vins 初始化部分使用了 ceres 做 sfm，所以我们还是需要依赖 ceres. 
    Download an older version (https://ceres-solver.googlesource.com/ceres-solver/+archive/facb199f3eda902360f9e1d5271372b7e54febe1.tar.gz)
    Install by following http://ceres-solver.org/installation.html

### 编译代码

```c++
mkdir vins_course
cd vins_course
git clone https://github.com/HeYijia/VINS-Course
sed -i 's/++11/++14/g' CMakeLists.txt
mkdir build 
cd build
cmake ..
make -j4
```

### 运行
#### 1. CurveFitting Example to Verify Our Solver.
```c++
cd bin
./testCurveFitting 
```

#### 2. VINs-Mono on Euroc Dataset
```c++
cd bin
./run_euroc /home/dataset/EuRoC/MH-05/mav0/ ../config/
```
![vins](doc/vins.gif)

#### 3. VINs-Mono on Simulation Dataset (project homework)

you can use this code to generate vio data.

```c++
https://github.com/HeYijia/vio_data_simulation
```

#### 4. Validation Results
[evo package](https://github.com/MichaelGrupp/evo)
```c++
evo_ape euroc euroc_mh05_groundtruth.csv pose_output.txt -a -p
```

![results](doc/results.png)

### Licence

The source code is released under GPLv3 license.

We are still working on improving the code reliability. For any technical issues, please contact Yijia He <heyijia_2013@163.com> , Xiang Gao <https://github.com/gaoxiang12> or Huakun Cui<https://github.com/StevenCui>.

For commercial inquiries, please contact Song Zhao <zhaosong@shenlanxueyuan.com>

### 感谢

我们使用了港科大沈老师组的 [VINS-Mono](https://github.com/HKUST-Aerial-Robotics/VINS-Mono) 作为基础代码，非常感谢该组的工作。

