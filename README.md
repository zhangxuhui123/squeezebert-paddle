# squeezebert-paddle


## 权重转换 && 权重下载
1. 从https://huggingface.co/squeezebert 下载hg的权重到models对应的目录下
2. ```python convert_torch_to_paddle.py```

转好的模型链接: https://pan.baidu.com/s/1Jis7In0veo4ODae5OR_FqA 提取码: p5bk

## 前向传播精度和速度对比
```
python compare.py

# model_name: squeezebert-uncased
# mean difference: 8.8708525e-08
# max difference: 6.556511e-07
#耗时对比 squeeze paddle  cost 43.851375579833984,  squeeze torch cotst 
48.86937141418457, bert cost 51.83529853820801


# model_name: squeezebert-mnli
# mean difference: 1.12165566e-07
# max difference: 7.4505806e-07

# model_name: squeezebert-mnli-headless
# mean difference: 1.12165566e-07
# max difference: 7.4505806e-07

```

## QQP数据集合效果 
### 运行步骤
在models/squeezebert-mnli-headles复制一份config.json,改名为model_config.json
```
export CUDA_VISIBLE_DEVICES=0
export TASK_NAME="QQP"

nohup python -u ./run_glue.py --model_type squeezebert --model_name_or_path ./models/squeezebert-mnli-headless --task_name QQP --batch_size 16 --learning_rate 4e-5 --num_train_epochs 5  --logging_steps 10 --save_steps 2000 --output_dir ./tmp/QQP/ --device gpu --lr_scheduler 1 --seed 5
```
### *运行结果*
```
acc and f1: 0.8936136479314183, eval done total : 196.82215237617493 s

```
|acc and f1|
| :----:|
|0.8936|
### 训练日志
见train_log.txt