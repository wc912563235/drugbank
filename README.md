# drugbank
这是一个为知识图谱而准备的数据抽取程序集。

简介：为了制作知识图谱，需要将公开的药物数据库drugbank中的数据提取后做成能导入nebulagraph的格式。

因xml文件过大无法上传至github，可在 https://go.drugbank.com/releases/latest 自行下载，解压后放入download文件夹即可。

# 文件介绍
process.ipnb：将公开药物数据库drugbank的数据分为了drug，target，pathway三类，输出为dataframe，重命名为可导入nebula graph的格式，最后输入到了data文件夹中。

extra_sequence处理：对多个fasta文件进行了提取与合并，最后融合到了drug和target中。

最终处理结果

如图所示，最终得到了3份节点文件，2份关系文件。

药物drug_ex.csv，靶点target_ex.csv，pathway:pathway.csv，关系:drug_target.csv,drug_pathway.csv。

![image](https://user-images.githubusercontent.com/48423282/223675175-fa2deef8-f888-4c28-a158-46e5cc01bee6.png)

# drugbank介绍
DrugBank Online 是一个全面的、免费访问的在线数据库，其中包含有关药物和药物靶点的信息。

权限：需要申请

![image](https://user-images.githubusercontent.com/48423282/223675410-b9cc9b9d-b97a-40c8-9286-9f65bb700f39.png)

# 数据构成
Xml文件类似于树形图，使用ElementTree包来解析文件的包含关系可以看做右图的树性结构，其中drug对应左图complextype name中的drug，后面的element的name可以看做是属性的分支。

根据xml文件的包含关系的特性，使用python的ElementTree包对原文件进行读取，定义xml文件的提取路径后，就使用程序进行遍历，读取了。

![image](https://user-images.githubusercontent.com/48423282/223675500-617ec763-41a9-4a4d-b916-a26607fe2ba6.png)
![image](https://user-images.githubusercontent.com/48423282/223675506-0d9d23c3-b356-40b6-85c5-58a7e0699f50.png)

# 确认数据处理方案
1,提取full database为三份文件,target,drug,drug-target。

2,增加pathway信息，单独作为一个文件，增加drug-pathway的关系文件。

3,从sequence的额外文件中提取出信息合并到主文件中。

![image](https://user-images.githubusercontent.com/48423282/223675631-01e048d4-90e4-4b1b-8ee3-c0cd77dfa749.png)
