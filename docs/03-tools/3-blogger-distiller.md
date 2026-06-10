# 博主内容蒸馏 - Blogger Distiller

## 一、工具简介

**Blogger Distiller** 是一款开源的博主内容分析工具，可以提取博主的写作风格，并使用 AI 改写生成新内容。

**GitHub 地址**：https://github.com/otter1101/blogger-distiller

### 核心功能
- 博主风格分析（语言习惯、叙事结构）
- 内容结构提取（爆款规律）
- AI 改写生成（保持风格一致性）
- 批量内容生产

---

## 二、安装与配置

### 1. 下载安装

```bash
# 克隆仓库
git clone https://github.com/otter1101/blogger-distiller.git

# 安装依赖
cd blogger-distiller
pip install -r requirements.txt

# 配置 API Key（支持 OpenAI / Claude 等）
cp config.example.yaml config.yaml
# 编辑 config.yaml 填入你的 API Key
```

### 2. 配置说明

```yaml
# config.yaml 示例
api:
  provider: "openai"  # 或 "anthropic"
  api_key: "your_api_key_here"
  model: "gpt-4"      # 或 "claude-3-sonnet"

distill:
  min_posts: 10       # 最少分析帖子数
  style_weight: 0.7  # 风格保留权重
  content_weight: 0.3 # 内容创新权重
```

---

## 三、使用流程

### Step 1：采集博主内容

使用 [RedBox](./2-redbox.md) 采集目标博主数据：

```bash
# 采集博主内容并导出
python redbox.py export --user_id="博主ID" --format=json --output=blogger_data.json
```

### Step 2：蒸馏博主风格

```bash
# 启动蒸馏工具
python distiller.py distill --input=blogger_data.json --output=style_profile.json
```

**输出内容包括**：
```json
{
  "writing_style": {
    "language_tone": "亲切、口语化",
    "sentence_structure": "短句为主，善于用问句",
    "punctuation_habits": "爱用省略号...",
    "emoji_usage": "使用频率高，😄😂🙄"
  },
  "content_patterns": {
    "title_patterns": ["X怎么做", "我是如何X的", "X是什么体验"],
    "opening_style": "以个人经历开头",
    "structure": "问题-分析-解决方案",
    "closing_style": "引导互动（评论区见）"
  },
  "topics": ["留学申请", "雅思备考", "英国生活"],
  "tags": ["留学", "英国", "雅思", "offer"]
}
```

### Step 3：AI 改写生成

```bash
# 使用蒸馏的风格生成新内容
python distiller.py generate \
  --style=style_profile.json \
  --topic="英国留学申请" \
  --output=generated_content.json
```

**生成内容示例**：
```json
{
  "title": "双非均分75如何拿到UCL offer？我的argue经验分享",
  "content": "作为曾经的双非选手...",
  "tags": ["留学", "英国", "UCL", "argue"],
  "style_notes": "保持了博主的口语化风格，短句为主"
}
```

---

## 四、实战应用

### 应用场景 1：素人号内容生产

```
背景：需要批量生产素人号内容
方案：
1. 采集留学类优质博主笔记
2. 蒸馏博主风格
3. AI 生成新内容（替换背景为海恒）
4. 使用 AntBrowser 发布
```

### 应用场景 2：专业号爆款模仿

```
背景：专业号需要提升互动率
方案：
1. 采集同类爆款笔记
2. 分析爆款规律
3. 使用蒸馏工具生成高互动标题
4. 结合海恒真实案例发布
```

---

## 五、配合工具链

```
RedBox（采集博主数据）
    ↓
Blogger Distiller（蒸馏风格）
    ↓
AI 生成新内容
    ↓
AntBrowser（多账号发布）
    ↓
小红书（发布内容）
```

---

## 六、参数调优建议

| 参数 | 说明 | 调整建议 |
|------|------|----------|
| style_weight | 风格保留程度 | 素人号用 0.8，专业号用 0.6 |
| content_weight | 内容创新程度 | 需要大量生产时提高到 0.5 |
| min_posts | 分析帖子数量 | 越多风格越准确，建议 20+ |

---

## 七、常见问题

### Q1：生成内容太机械怎么办？
```
解决方案：
1. 提高 style_weight 到 0.8
2. 增加口语化词汇
3. 手动修改生成内容
4. 多次生成选择最优
```

### Q2：如何保持内容原创性？
```
解决方案：
1. 多个博主风格混合
2. 加入海恒真实案例
3. 替换地域/学校等元素
4. 人工审核后发布
```

### Q3：API 成本如何控制？
```
建议：
1. 批量处理减少 API 调用
2. 使用 GPT-3.5 代替 GPT-4
3. 缓存已蒸馏的风格
4. 合理设置采集数量
```

---

## 八、使用示例

```bash
# 完整流程示例

# 1. 采集数据
python redbox.py collect --keyword="英国留学" --limit=50

# 2. 蒸馏风格
python distiller.py distill --input=collected.json --output=uk_style.json

# 3. 生成内容
python distiller.py generate \
  --style=uk_style.json \
  --topic="UCL申请" \
  --title_template="X如何申请UCL" \
  --output=content_batch.json

# 4. 批量导出
python distiller.py export --input=content_batch.json --format=markdown
```

> 生成的内容可以在[素材库](./04-resources/1-material-links.md)中整理，配合图片素材发布