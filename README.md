# opencv-python-tutorial

opencv python的一站式使用工具

pycv-utils提供对opencv的使用类，方法，参数的直接说明，可以直接查看opencv内的全部的使用说明文档，其功能在使用级别上等价于\_\_doc\_\_()魔法方法，与自身的的doc不同的是，本项目补充了各个参数的详细用法与指标，对方法所采用的数学原理也提供了描述，增加了测试用例的说明，使opencv的使用更加便捷，对各个api的功能描述更加适配，可以极大加速非CV开发人员的上手时间。此外utils提供了cv各个同类算法的算法比较模块，可以通过自主定义来查看各个算法在实际开发场景中的执行与指标优劣，减少对比不同算法量化效果所花费的时间。另外utils提供了对cv算法的可视化调节支持，通过可视化界面对算法各个参数的调整效果有明显的参考意义。

本仓库包含以下内容：

- pycv-utils的实际代码与相关的辅助支持文件
- pypi提交与算法安装的描述与setup文件
- docker提交的模板文件与相关配置文件
- 示例说明文件README.md
- 项目相关的文档与使用说明文件



## 内容列表

- [背景](#背景)
- [注意](#注意)
- [安装](#安装)
- [使用说明](#使用说明)
- [维护者](#维护者)
- [如何贡献](#如何贡献)
- [使用许可](#使用许可)



## 背景

opencv是一个基于BSD许可（开源）发行的跨平台计算机视觉和机器学习软件库，其功能十分强大，在处理图像数据与进行相关机器学习计算中提供了良好的支持，是数字处理人员的必备开发工具，opencv由一系列的C函数组成，虽然提供了python的接口，但是并不能像原生python一样进行内部调试，其文档与相关异常也难以符合python的开发习惯，同时opencv提供了大量的数字图像处理算法，每中算法具有不同的使用场景和优势，在对算法进行量化处理时较为困难，综合以上的问题，为提高python下的opencv接口的易用性，降低开发难度，本项目面向所有开发人员提供一套基于opencv的工具包。



## 注意

- 本项目正在与imutils开源工具包作者进行交流，合并双方工具包的功能，以形成一个具有完善功能的总工具包，各自弥补不足，方便项目的具体使用，在合并项目之前，本项目代码，pypi，docker镜像不再提供维护。
- 如果您正在使用本项目的pypi或者docker历史工具包，请继续保留您的本地副本，在项目重新纳入版本管理前，原始版本项目不再提供三方拉取与维护支持。
- 项目合并工作正在进行，预计完成时间2020年10月01日，期待您的贡献。



## 安装

- 环境依赖

  ```python
  Python (3.6, 3.7, 3.8, 3.9)
  opencv-python==3.4.2.17
  opencv-contrib-python==3.4.2.17
  PySide2==5.15.2
  prettytable==2.1.0
  ```

- 通过pypi进行安装，您可以快速通过wheel进行项目构建，这里建议您使用虚拟环境进行安装配置使用，本项目所依赖的opencv为3.4版本，不同版本的opencv接口具有较大差异，预计项目在下一个版本中支持opencv4.x

  ```python
  pip install opencv-python-tutorial
  ```

- 如果您只是想要当做学习或者教学使用，可以通过docker镜像进行拉取使用

  ```dockerfile
  docker pull jinming/opencv-python-tutorial:v2.0
  ```

  

## 使用说明

- 快速开始，使用项目的文档说明功能，您只需要导入相关cv的方法或者类模块，进行说明即可，如果您想不使用对象进行查看，使用同名字符串也可以达到相同的效果，例如：

  ```python
  from cv2 import cv2 as cv
  from pycv_uitls import cv_docs as docs
  from pycv_uitls import cv_find as find
  
  # 等价于 print(docs("cv.threshold"))
  print(docs(cv.threshold))
  """
  输出：
  	>>> ret, dst = cv2.threshold(src, thresh, maxval, type)
  	
      设置固定级别的阈值应用于多通道矩阵
          例如，将灰度图像变换二值图像，或去除指定级别的噪声，或过滤掉过小或者过大的像素点；
          图像的阈值处理一般使得图像的像素值更单一、图像更简单；
          阈值可以分为全局性质的阈值，也可以分为局部性质的阈值，可以是单阈值的也可以是多阈值的。
      Argument:
          src: 原图像,必须是单通道
          dst: 目标图像
          thresh: 阈值,取值范围0～255
          type: 指定阈值类型；下面会列出具体类型；
          maxval: 当type指定为THRESH_BINARY或THRESH_BINARY_INV时,需要设置该值,取值范围0～255；
      type可用参数说明:
          cv.THRESH_BINARY | cv.THRESH_OTSU 大津法,全局自适应阈值,参数0可改为任意数字但不起作用
          cv.THRESH_BINARY | cv.THRESH_TRIANGLE 全局自适应阈值,参数0可改为任意数字但不起作用，适用于单个波峰
          cv.THRESH_BINARY 若自定义阈值为150,大于150的是白色,小于的是黑色
          cv.THRESH_BINARY_INV 若自定义阈值为150,大于150的是黑色,小于的是白色
          cv.THRESH_TRUNC 若自定义阈值为150,大于150的是改为150,小于150的保留
          cv.THRESH_TOZERO 若自定义阈值为150,小于150的是改为150,大于150的保留
      返回值: 
          ret: 与参数thresh一致
          dst: 结果图像
  """
  
  # TODO 模糊查询，可通过中文或者英文释义进行查询，建议使用英文释义
  # 等价于 print(find("轮廓"))
  print(find("contour"))
  """
  输出：
  	["contourArea", "drawContours", "findContours", "isContourConvex"]
  """
  ```

- 本项目也支持相似算法的对比，通过量化指标来对比不同函数方法之间的区别于实际效果，通过实际指标可以迅速完成对实际应用场景的需求算法选择，例如：

  ```python
  from cv2 import cv2 as cv
  from pycv_uitls import cv_vs as compare
  
  # 下面例子是比较图像相似度算法，可以通过dir方法查看compare的可用参数
  # 支持导入数据，支持指定算法，默认使用已有的用例进行全算法测试
  print(compare('similarity'))
  ```

  ![](.\pics\compare.jpg)

- 本项目支持对原opencv算法的增强执行，例如原算法中均为原子型算法，所获取的效果并不能达到所需要的精度结果，通过相应的增强算法，可以大大弥补原始算法中对于图像质量不佳，或者某些临界判断不出的问题，例如：通过霍夫曼检测直线会出现线断续的问题，部分原因在于原始的线临界值没有达到阈值要求，虽然通过一些形态学或者色彩通道处理能够到达应用效果，但却增加编码难度，算法增强模块提供了对原始算法的改进有优化逻辑，例如如下，可以看到检测的效果被有效的增强了。

  ```python
  from cv2 import cv2 as cv
  from pycv_uitls import cv_enhance as eh
  
  # 以棋盘格检测为例，使用opencv进行检测步骤为
  # cv.findChessboardCorners  发现棋盘角点
  # cv.cornerSubPix  亚像素级检测，提升精度
  # 对于图像倾斜，非结构棋盘格的形式，或者质量不高的图像无法进行检测，增强后效果
  eh_findChessboardCorners = eh(findChessboardCorners)
  cv.drawChessboardCorners(eh_findChessboardCorners(img))
  ```

  <img src=".\pics\eh.jpg" style="zoom:30%;" />

- 本项目支持cv算法的可视化展示，通过可视化界面调节参数，可以动态的观测到该算法所变化参数的实际效果，界面使用pyqt进行构建，因此需要PySide2库的支持，例如：

  ```python
  from cv2 import cv2 as cv
  from pycv_uitls import cv_visual as show
  
  show(cv.threshold(src, thresh, maxval, type))
  ```

  <img src=".\pics\show.jpg" style="zoom:50%;" />



## 维护者

- qiao_jinming@foxmail.com
- [@Jinming Qiao](https://github.com/QiaoJinming)



## 如何贡献

非常欢迎您的加入！请提一个 Issue或者提交一个 Pull Request。



## 使用许可

[MIT](LICENSE) ©Jinming Qiao

