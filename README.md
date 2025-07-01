# 遥感目标检测样本处理流水线

这是一个用于处理遥感目标检测数据集的完整流水线工具。该工具可以帮助你从原始的遥感影像和点标注文件开始，生成用于目标检测模型训练的COCO格式数据集。

## 功能特点

1. **影像裁剪**：根据点标注自动裁剪小块影像
2. **矢量生成**：为裁剪的影像生成对应的矢量文件，支持多类别标注
3. **数据增强**：通过多种增强方法扩充样本数量
4. **COCO格式转换**：将处理后的数据集转换为标准COCO格式
5. **可视化工具**：支持数据集的可视化和质量检查

## 安装依赖

```bash
pip install -r requirements.txt
```

## 目录结构

```
.
├── modules/                # 模块目录
│   ├── step1_image_clipper.py      # 影像裁剪模块
│   ├── step2_vector_generator.py   # 矢量生成模块
│   ├── step3_data_augmentation.py  # 数据增强模块
│   ├── step4_coco_converter.py     # COCO格式转换模块
│   └── step5_visualization.py      # 可视化模块
├── config.py              # 配置文件
├── utils.py              # 通用工具函数
├── main.py               # 主程序
└── requirements.txt      # 依赖列表
```

## 使用方法

该工具支持分步执行，每个步骤都可以独立运行：

1. **裁剪影像**：
```bash
python main.py --step 1 --input-image path/to/image.tif --input-points path/to/points.shp
```

2. **生成矢量**：
```bash
python main.py --step 2 --input-points path/to/points.shp
```

3. **数据增强**：
```bash
python main.py --step 3 --input-image path/to/clipped_image.tif --input-vector path/to/vectors.shp
```

4. **转换COCO格式**：
```bash
python main.py --step 4 --input-vector path/to/augmented_vectors.shp
```

5. **可视化结果**：
```bash
python main.py --step 5 --dataset-dir path/to/coco_dataset
```

## 输出目录结构

```
output/
├── clipped_images/    # 步骤1的输出：裁剪后的影像
├── vectors/          # 步骤2的输出：生成的矢量文件
├── augmented/        # 步骤3的输出：数据增强结果
│   ├── images/      # 增强后的影像
│   └── vectors/     # 增强后的矢量
├── coco_dataset/    # 步骤4的输出：COCO格式数据集
│   ├── images/      # 训练/验证/测试集影像
│   └── labels/      # COCO格式标注文件
└── visualization/   # 步骤5的输出：可视化结果
```

## 多类别标注说明

在ArcGIS中进行多类别样本标注时，建议：

1. 为每个类别创建单独的图层
2. 使用不同的颜色和样式区分各个类别
3. 在属性表中添加类别字段
4. 导出时保持类别信息完整

## 注意事项

1. 确保输入影像和矢量文件使用相同的坐标系
2. 建议先处理小批量数据进行测试
3. 数据增强参数可在config.py中根据实际需求调整
4. 定期检查生成的样本质量
5. 每个步骤的输出结果都保存在相应目录中，可以作为下一步骤的输入

## 许可证

MIT License 