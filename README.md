# F053 投标推荐可视化系统+推荐算法vue+flask+爬虫

> 完整项目收费，可联系QQ: 81040295 微信: mmdsj186011 注明从github来的，谢谢！
也可以关注我的B站： 麦麦大数据 https://space.bilibili.com/1583208775
> 
> 关注B站，私信获取！   [麦麦大数据](https://space.bilibili.com/1583208775)
> 编号:  F053
## 视频
《待发布》
## 1 系统简介

系统简介：本系统是一个基于**Vue+Flask+MySQL**构建的**投标推荐可视化系统**。其核心功能围绕对招标投标数据的深度分析、智能推荐与可视化展示。主要功能模块包括：**用户登录注册、投标信息查询、基于数据分析的推荐、关键词词云展示、数据爬取与清洗**。

## 2 功能设计

该系统采用前后端分离的B/S架构模式，基于**Vue+Flask+MySQL**技术栈实现。前端通过Vue.js框架搭建响应式界面，结合Vue-Router进行页面路由管理，Axios实现与后端的异步数据交互，利用ECharts等组件提供丰富的数据可视化效果。Flask后端负责构建RESTful API服务，通过**SQLAlchemy**操作**MySQL**数据库存储用户、招标项目等结构化数据。

在**投标推荐**功能方面，系统采用**数据分析算法**对项目数据进行挖掘，找出相似项目或潜在风险，从而为用户提供智能化的投标建议。
### 2.1 系统架构图
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/65f21c52b8c8464c848d76cb8d7fdebb.png)
### 2.2 功能模块图
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/ecddc1d744ea456490920226d77e3a40.png)
主要功能模块有：

1.  **用户登录 & 注册**
2.  **投标信息查询**
3.  **数据爬取**
4.  **数据分析**
5.  **词云展示**
6.  **数据清洗**

### 3.1 登录 & 注册
登录注册做的是一个可以切换的登录注册界面，点击去登录后者去注册可以切换。登录需要验证用户名和密码是否正确。
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/d8a024ca989346f1a74176db52a9d8f3.png)
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/9a9b24780c1344a48712784100f7b601.png)
### 3.2 投标算法推荐 && 信息查询
使用双算法进行招投标项目的推荐：
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/dfe033d616f5464089a72eca19fdfa2b.png)
用户可以通过该功能，根据关键词（如项目名称、地区、行业）查询和浏览详细的投标项目信息，为参与投标提供决策依据。
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/6803cb1261c34ab780e3449a76a8ec3f.png)
### 3.3 数据分析
系统对已有的投标项目数据进行统计分析，如项目数量趋势、行业分布、地域分布等。分析结果通过图表形式展现，帮助用户理解市场动态。
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/7fc366284f7a4c38b9ca8fa38c74d0fd.png)
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/b61b3fcb57eb42afaa29efff7fcc0e7d.png)
招标金额分析：
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/6deb84a485544fcfa6ba4ac62a21ab47.png)
### 3.4 词云展示
系统对投标项目中的高频关键词进行提取，并生成词云图。词云的视觉效果直观地展示了当前市场关注的热点话题和行业术语。
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/2779b37d923d4e40a039cf34384c3c65.png)
### 3.5 数据爬取
管理员负责系统的数据源管理。该模块支持从网络上主动爬取最新的、公开的招标投标信息，并将其存入数据库，保证了数据的时效性和完整性。
（见爬虫部分）
### 3.6 数据清洗
在数据爬取后，系统对获取的原始数据进行清洗，包括去除重复项、处理缺失值、标准化格式等，以确保数据库中数据的质量和可用性。
（见爬虫部分）
### 3.7 管理员
管理员拥有系统的最高权限，负责核心的系统维护和数据管理，包括用户权限管理、数据爬取、数据清洗和系统配置。
（见爬虫部分）
### 3.8 个人设置
个人设置方面包含了用户信息修改、密码修改功能。
用户信息修改中可以上传头像，完成用户的头像个性化设置，也可以修改用户其他信息。

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/98e8ec2af5d0471f8862d89e935a81e9.png)
上传身份证完成实名认证。
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/a8376035962940ea83227e9cf48aeeb1.png)
## 4 程序核心算法代码
### 4.1 代码说明

代码介绍：

### 4.2 流程图

### 4.3 代码实例

```python
# 示例：使用SQLAlchemy连接MySQL查询招标项目
from sqlalchemy import create_engine, text
from sqlalchemy.orm import sessionmaker

# 创建数据库连接引擎
engine = create_engine('mysql+mysqlconnector://user:password@localhost:3306/tender_system')

# 创建会话
Session = sessionmaker(bind=engine)
session = Session()

# 执行SQL查询，例如查询特定行业（如“建筑工程”）的项目
sql = text("SELECT * FROM projects WHERE industry = :industry")
results = session.execute(sql, {"industry": "建筑工程"}).fetchall()

# 输出查询结果
for row in results:
    print(row)
```

```sql
-- 示例：创建投标项目表
CREATE TABLE projects (
    id INT AUTO_INCREMENT PRIMARY KEY,
    project_name VARCHAR(255) NOT NULL,
    industry VARCHAR(100),
    location VARCHAR(255),
    tender_start_date DATE,
    tender_end_date DATE,
    total_amount DECIMAL(10, 2),
    description TEXT
);
```
