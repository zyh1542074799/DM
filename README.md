# 刀模管理系统 - 云端数据库版

## 功能特性

✅ **刀模信息管理** - 新增、编辑、删除、搜索
✅ **领用/归还** - 完整进出记录追踪
✅ **状态管理** - 空闲/领用中/样品 三种状态
✅ **操作日志** - 所有操作全程记录
✅ **Excel导入** - 一键导入现有数据
✅ **云端数据库** - SQLite持久化存储
✅ **响应式设计** - 手机电脑通用

## 技术架构

- **后端**: Python + Flask
- **数据库**: SQLite（云端持久化）
- **前端**: HTML5 + CSS3 + JavaScript
- **部署**: Railway / Render

## 目录结构

```
刀模系统云端版/
├── app.py          # Flask 后端 API
├── index.html      # 前端页面
├── requirements.txt # Python 依赖
├── Procfile        # Railway 部署配置
├── start.sh        # 启动脚本
└── README.md       # 本说明文件
```

## 快速部署到 Railway（免费）

### 步骤 1：打包项目
将 `刀模系统云端版` 文件夹压缩成 zip

### 步骤 2：创建 Railway 账号
访问 https://railway.app 注册（可用 GitHub 登录）

### 步骤 3：新建项目
1. 点击 "New Project" → "Deploy from GitHub repo" 或 "Empty Project"
2. 如果选 Empty Project，点击 "Add a Service" → "Empty Service"

### 步骤 4：上传代码
1. 在 Railway 项目中，点击刚创建的服务
2. 选择 "Settings" → "Source"
3. 使用 Railway CLI 或直接上传：
   ```bash
   # 安装 Railway CLI
   npm install -g @railway/cli
   
   # 登录
   railway login
   
   # 进入项目目录
   cd 刀模系统云端版
   
   # 初始化并部署
   railway init
   railway up
   ```

### 步骤 5：配置环境变量（可选）
在 Railway Settings 中设置：
- `PORT`: 5000

### 步骤 6：访问
部署成功后，Railway 会分配一个域名，如：`xxx.railway.app`

## 替代部署方案

### Render（免费）
1. 注册 https://render.com
2. 创建 "Web Service"
3. 连接 GitHub 仓库或直接上传代码
4. 设置：
   - Build Command: `pip install -r requirements.txt`
   - Start Command: `python app.py`

### Vercel + 外挂数据库
需要额外的数据库服务（推荐使用 Railway 自带的 PostgreSQL）

## 本地运行

```bash
cd 刀模系统云端版
pip install -r requirements.txt
python app.py
```

访问 http://localhost:5000

## API 接口

| 接口 | 方法 | 说明 |
|------|------|------|
| `/api/blades` | GET | 获取刀模列表 |
| `/api/blades` | POST | 新增刀模 |
| `/api/blades/<id>` | PUT | 更新刀模 |
| `/api/blades/<id>` | DELETE | 删除刀模 |
| `/api/borrow` | POST | 领用刀模 |
| `/api/return` | POST | 归还刀模 |
| `/api/records` | GET | 领用记录 |
| `/api/logs` | GET | 操作日志 |
| `/api/stats` | GET | 统计数据 |
| `/init-data` | POST | Excel导入 |

## 数据字段

| 字段 | 说明 |
|------|------|
| 编号 | 唯一标识（如 UC001） |
| 客户料号 | 客户提供的料号 |
| 裁切过的料号 | 历史裁切的料号记录 |
| 规格 | 产品规格 |
| 刀片类型 | 刀片材质类型 |
| 尺寸 | 刀模尺寸（数值） |
| 角度 | 刀模角度 |
| 穴数 | 一模几穴 |
| 数量 | 库存数量 |
| 累计裁切数 | 总使用次数 |
| 状态 | 空闲/领用中/样品 |
| 备注 | 其他备注 |

## 注意事项

1. SQLite 数据库文件 `blade_molds.db` 会自动创建
2. 部署到 Railway 时数据会持久保存
3. 如需重置数据，删除 `blade_molds.db` 后重启服务

## 初始数据

系统部署后可导入你提供的 Excel 文件，包含 69 个刀模数据。
