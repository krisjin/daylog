# 使用MXNet实现人脸识别
_**基于Modelarts SDK功能，利用MXNet引擎，端到端实现人脸识别项目的一站式开发**_


---

---

## 内容

1. [背景介绍](#背景介绍)
2. [环境配置](#环境配置)
3. [数据管理](#数据管理)
4. [本地训练](#本地训练)
5. [提交训练作业](#提交训练作业)
6. [模型管理](#模型管理)
7. [部署上线](#部署上线)
8. [在线测试](#在线测试)
9. [资源释放](#资源释放)

---


## 背景介绍

人脸识别是基于人脸视觉特征信息进行身份鉴别的计算机技术，用于门禁系统、人证核验、智能安防等领域。本notebook将展示利用MXNet构建深层神经网络，对图像中人脸进行身份识别， 并结合[ModelArts SDK功能](https://support.huaweicloud.com/usermanual-modelarts/modelarts_02_0001.html)端到端完成一站式开发部署 。主要内容包括:
* 基本的环境配置
* 数据集的管理，展示数据集信息
* 在本地构建神经网络，完成训练并进行测试输出
* 在云上创建训练作业
* 创建模型，并实现模型的在线部署
* 输入本地测试图片进行在线测试
* 释放本notebook生成的资源，包括作业、模型和服务






## 环境配置

本项目无需手动设置，所需的存储桶、目录等都由自动生成，配置内容包括：
* 定位项目源文件在容器中位置
* 当使用OBS类型的notebook/JupyterLab实例时，当前目录默认为mxnet_face_recognition




import os, sys
if os.getenv("JUPYTER_ENABLE_OBS") == "false":
    project_path = os.getcwd() + "/"
else:
    #OBS类型Notebook实例，默认example目录
    directory = "mxnet_face_recognition"
    project_path = os.environ['HOME'] + '/work/' + directory + "/"
sys.path.append(project_path)



##  数据管理

本项目所需的数据集格式为NXNet专用的rec格式，都存储在本地中。人脸识别数据集使用的是明星人脸图像集CelebFace，经过人脸3D对齐等操作制作成了适合分类模型训练的数据，每张图像的大小为112*112。





# 训练集和数据集本地路径
local_train_path = source_file_path + 'data/celeb_train.rec'
local_val_path = source_file_path + 'data/celeb_val.rec'





def parse_args():
    parser = argparse.ArgumentParser(description='Train face network')
    # 训练数据路径
    parser.add_argument('--data_dir', default='data',help='training set directory')
    # 训练模型输出路径
    parser.add_argument('--train_url', type=str, default=source_file_path+ 'ckpt',help='train path')
    # 训练epoch数量
    parser.add_argument('--num_epoch', type=int, default=5,help='training epoch size.')
    # 使用的ResNet卷积层层数
    parser.add_argument('--num_layers', type=int, default=18,help='specify network layer, 18 50 100')
    # 输入图像的大小，高、宽
    parser.add_argument('--image_size', default='112,112',help='specify input image height and width')
    # 训练开始的学习率大小
    parser.add_argument('--lr', type=float, default=0.005,help='start learning rate')
    # 权值衰减系数
    parser.add_argument('--wd', type=float, default=0.0005,help='weight decay')
    # 动量
    parser.add_argument('--mom', type=float, default=0.9,help='momentum')
    # 每一个GPU的batch size大小
    parser.add_argument('--per_batch_size', type=int, default=8, help='batch size in each context')
    # 训练样本大小
    parser.add_argument('--epoch_image_num', type=int, default=200,help='image size in one epoch')
    # 训练数据文件
    parser.add_argument('--train_file', type=str, default='celeb_train.rec',help='train')
    # 验证集文件
    parser.add_argument('--val_file', type=str, default='celeb_val.rec',help='val')
    # 分类数
    parser.add_argument('--num_classes', type=int, default=5,help='classes number')
    # 嵌入层神经元数量
    parser.add_argument('--num_embed', type=int, default=8,help='embedding number')
    # GPU数量
    parser.add_argument('--num_gpus', type=int, default=0,help='GPUs number')
    # 保存模型的频率
    parser.add_argument('--save_frequency', type=int, default=1,help='save frequency')
    #是否改变train url结构
    parser.add_argument('--export_model', type=bool, default=False,help='change train url to model,metric.json')
    args, _ = parser.parse_known_args()
    return args

args = parse_args()





## 模型管理
导入训练作业生成模型


exec_code = source_file_path + 'src/customize_service.py'
session.upload_data(base_bucket_path+'model/', exec_code)

model_path = base_bucket_path
model = estimator.create_model(model_algorithm = "face",
                               source_location = model_path,
                               execution_code = model_path + 'model/customize_service.py',
                               model_type="MXNet")






## 部署上线
将生成的模型部署上线




# 调用deploy接口部署模型, 生成Predictor对象
configs = [ServiceConfig(model_id=model.get_model_id(),weight="100",instance_count=1,specification="modelarts.vm.cpu.2u",envs={})]
predictor = estimator.deploy_predictor(service_name="face_recognition",configs=configs)


## 在线测试
对本地data目录下的test.png进行在线分类测试。 读者可以与本地训练的预测结果进行对比。




predict_result = predictor.predict(data= source_file_path + args.data_dir + '/test.png',data_type = "images")
print(predict_result)



