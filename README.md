# GF-7卫星数据产品真实性检验及综合评价技术项目程序

基于对GF-7真实性检验方法的研究开展GF-7真实性检验软件的设计及初步实现。软件开发过程中严格依照实施方案中的真实性检验技术路线进行，从软件灵活性、时间特性、精确性、故障处理、数据管理等方面进行规范化设计与开发，软件在windows10系统下基于python语言开发。GF-7数据模拟转换软件模块依据GF-7卫星数据特点，结合光谱仪的光谱响应函数和中心波长等参数实现数据的光谱维和空间维转换；GF-7间接反射率产品真实性检验模块利用转换后的数据的反射率产品和待真实性检验的GF-7反射率数据产品，结合两个数据产品的全局光谱曲线特征，通过分析其相关系数、光谱角等的一致性，通过均方根误差等评价其反射率产品的精度；GF-7植被叶面积指数产品真实性检验模块通过对实测或其他卫星数据的植被叶面积指数产品和待真实性检验的GF-7植被叶面积指数产品间的总体精度OA、分类一致系数kappa等精度指标的一致性检验。下面从软件构成、技术流程、功能实现等几个方面简要论述。

1界面、开发语言及环境
（1）客户端环境
-	系统平台：Windows 10；
-	处理器： Intel (R) Core(TM) i7-9750H CPU @2.60GHZ；
-	内存：16G
-	存储设备：固态硬盘（1T）
（2）软件模块开发环境
真实性检验软件模块是在Windows 10系统环境下基于vscode开发平台的python语言编写，需要调用gdal、numpy、math、sklearn等外部库，具体开发环境与配置如下：
	开发语言： python；
	操作系统： Windows 10；
	开发平台： pycharm；
	处理器： Intel (R) Core(TM) i7-9750H CPU @2.60GHZ；
	内存：16G；
	硬盘：固态硬盘（1T）；
（3）界面
GF-7真实性检验软件主界面采用Pyqt5开发，在单机环境下通过界面选择输入输出文件路径，填写参数，后台将参数传递给相应的计算函数完成计算，如存在错误信息将弹出错误对话框。程序已全部开源，在集群环境下，可通过调用可执行程序+XML参数形式进行部署，支持自定义界面，后台采用XML传参。

2软件部署与运行
软件模块提供单机版和集群版两种部署方式，单机版直接将安装程序配置在英文目录下，启动main.exe即可。集群环境下，可以通过调用相应功能的可执行程序，结合具有固定格式的XML文本完成参数的传递。如下表所示：
 
3软件构成
包含数据尺度转换、间接反射率真实性检验、直接反射率真实性检验、专题产品真实性检验和光谱特征真实性检验五个功能。
 
4软件主要功能及参数
 1)	数据尺度转换
由于不同成像载荷获取的数据的空间分辨率、光谱分辨率及光谱特征均不相同，将实测光谱数据和机载或星载遥感数据转换为和GF-7具有一样的空间分辨率和光谱分辨率的遥感数据是实现对GF-7数据产品的真实性检验的必要步骤。GF-7数据模拟转换模块通过对输入数据进行基于光谱响应函数和中心波长的光谱重采样及空间分辨率的重采样实现数据的模拟转换。

2)	  间接反射率产品真实性检验
间接反射率产品真实性检验模块针对与GF-7相似载荷反演的反射率产品进行验证。通过对比转换后的数据和待真实性检验的GF-7反射率数据的全局/局部光谱曲线和光谱特征参数，计算反射率数据产品之间的光谱相关系数、光谱角及欧氏距离等评价指标，实现GF-7反射率产品真实性检验。

3)	  直接反射率产品真实性检验
直接反射率产品真实性检验模块针对地面实测点的反射率数据对GF-7反射率产品进行验证。通过对比采样点位置上实测反射率和待真实性检验的GF-7反射率数据的全局/局部光谱曲线，计算反射率数据产品之间的光谱相关系数、光谱角及欧氏距离等评价指标，实现GF-7反射率产品真实性检验。

4)	  专题产品真实性检验
用于实现GF-7与相似载荷在NDVI，叶面积指数等专题产品的真实性检验，可设定检验的空间区域，评价指标采用总体精度OA和分类一致性系数Kappa系数。

5)	  专题产品真实性检验
对于采用高光谱数据作为参考数据进行真实性检验的情况下，还提供了针对光谱特征的真实性检验，评价指标采用吸收位置、吸收深度、相关系数、光谱角。
