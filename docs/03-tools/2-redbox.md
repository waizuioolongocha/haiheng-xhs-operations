# 对标账号采集 - RedBox

## 一、工具简介

**RedBox** 是一款开源的小红书数据采集工具，专门用于采集竞品账号的笔记数据。

**GitHub 地址**：https://github.com/Jamailar/RedBox

### 核心功能
- 按账号采集笔记数据
- 按关键词采集内容
- 导出数据（Excel/JSON）
- 爆款内容分析

---

## 二、安装与配置

### 1. 下载安装

```bash
# 克隆仓库
git clone https://github.com/Jamailar/RedBox.git

# 安装依赖
cd RedBox
pip install -r requirements.txt

# 启动
python redbox.py
```

### 2. 配置说明

| 配置项 | 说明 |
|--------|------|
| Cookie 配置 | 登录小红书获取 Cookie |
| 采集间隔 | 建议 3-5 秒（防封） |
| 数据存储 | 本地 SQLite 数据库 |

---

## 三、采集操作指南

### 1. 按账号采集

```python
# 示例代码
from redbox import RedBox

rb = RedBox()
# 登录 Cookie
rb.set_cookie("your_cookie_here")

# 采集指定账号
rb.collect_by_user(user_id="账号ID", limit=50)
```

### 2. 按关键词采集

```python
# 采集留学相关关键词
rb.collect_by_keyword(keyword="英国留学申请", limit=100)
rb.collect_by_keyword(keyword="留学中介", limit=100)
```

---

## 四、数据分析

### 采集数据字段

| 字段 | 说明 |
|------|------|
| 笔记标题 | 标题文本 |
| 笔记内容 | 正文内容 |
| 点赞数 | 点赞数量 |
| 收藏数 | 收藏数量 |
| 评论数 | 评论数量 |
| 发布日期 | 发布时间 |
| 标签 | 笔记标签 |
| 作者 | 发布账号 |

### 爆款分析

采集完成后，使用 RedBox 内置分析功能：

```bash
# 分析爆款规律
python redbox.py analyze --type=top_liked

# 输出高赞笔记标题、标签、发布时间规律
```

---

## 五、在运营中的应用

### 1. 选题参考

通过采集数据发现：
- 哪些选题点赞高
- 什么时间发布效果好
- 热门标签有哪些

### 2. 内容模仿

爆款内容分析后：
- 提取标题结构
- 分析封面风格
- 学习内容框架

### 3. 竞品监控

定期采集竞品账号：
- 监测内容发布频率
- 跟踪爆款内容
- 分析互动数据变化

---

## 六、配合使用工具链

```
RedBox（采集数据）
    ↓
人工分析爆款规律
    ↓
Blogger Distiller（蒸馏博主风格）
    ↓
AI 改写生成内容
    ↓
AntBrowser（多账号发布）
```

---

## 七、常见问题

### Q1：Cookie 过期怎么办？
```
解决方案：
1. 重新登录小红书网页版
2. 获取新的 Cookie
3. 更新 RedBox 配置
```

### Q2：采集被限制怎么办？
```
解决方案：
1. 降低采集频率（间隔 10 秒以上）
2. 使用多个 Cookie 轮换
3. 更换 IP
```

### Q3：数据导出格式？
```
支持格式：
- SQLite（本地数据库）
- JSON（结构化数据）
- CSV（Excel 可直接打开）
```