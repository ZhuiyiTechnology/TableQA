# 首届中文NL2SQL挑战赛数据集

赛题了提供约40,000条有标签数据作为训练集，5,000条数据作为验证集，10,000条无标签数据作为测试集。其中，5,000条测试集数据作为初赛测试集，自然语言问句对选手可见；5,000条作为复赛测试集，自然语言问句对选手不可见。

以训练集为例，其中包括了**train.json**、**train.tables.json**及**train.db**。

#### 数据说明
**train.json**文件中，每一行为一条数据样本。数据样例及字段说明例如下：

```json
{
     "table_id": "a1b2c3d4", # 相应表格的id
     "question": "世茂茂悦府的套均面积是多少？", # 自然语言问句
     "sql":{ # 相应SQL
        "sel": [7], # SQL选择的列
        "agg": [0], # 选择的列相应的聚合函数, '0'代表无
        "cond_conn_op": 0, # 条件之间的关系
        "conds": [
            [1,2,"世茂茂悦府"] # 条件列, 条件类型, 条件值，col_1 == "世茂茂悦府"
        ]
    }
}
```

SQL的表达字典说明：

```python
op_sql_dict = {0:">", 1:"<", 2:"==", 3:"!="}
agg_sql_dict = {0:"", 1:"AVG", 2:"MAX", 3:"MIN", 4:"COUNT", 5:"SUM"}
conn_sql_dict = {0:"", 1:"and", 2:"or"}
```

**train.tables.json**文件中，每一行为一张表格数据。数据样例及字段说明例如下：
```json
{
    "id":"a1b2c3d4", # 表格id
    "name":"Table_a1b2c3d4", # 表格名称
    "title":"表1：2019年新开工预测 ", # 表格标题
    "header":[ # 表格所包含的列名
        "300城市土地出让",
        "规划建筑面积(万㎡)",
        ……
    ],
    "types":[ # 表格列所相应的类型
        "text",
        "real",
        ……
    ],
    "rows":[ # 表格每一行所存储的值
        [
            "2009年7月-2010年6月",
            168212.4,
            ……
        ]
    ]
}
```
**tables.db**为sqlite格式的数据库形式的表格文件。各个表的表名为**tables.json**中相应表格的name字段。

为避免部分列名中的特殊符号导致无法存入数据库文件，表格中的列名为经过归一化的字段，col_1, col_2, …。

#### 联系方式
如有问题，请联系 杨雪峰 ryan@wezhuiyi.com、孙宁远 waynesun@wezhuiyi.com

#### 使用权限
本数据开源给学术界推动技术进步， 严禁商业使用与未授权公开转发. 如果您在研究中使用了本数据集，请引用
https://arxiv.org/abs/2006.06434

@misc{sun2020tableqa,
    title={TableQA: a Large-Scale Chinese Text-to-SQL Dataset for Table-Aware SQL Generation},
    author={Ningyuan Sun and Xuefeng Yang and Yunfeng Liu},
    year={2020},
    eprint={2006.06434},
    archivePrefix={arXiv},
    primaryClass={cs.DB}
}