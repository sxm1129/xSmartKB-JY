# xSmartKG 快速部署套件 (xSmarkKB-JY)

这是一个基于 Docker 的一键部署套件，包含了 xSmartKG 的所有核心组件：
- **Frontend**: Web 交互界面
- **Backend**: DB-GPT 核心服务（已集成 OCR 补丁）
- **MySQL**: 关系型数据库 (8.0)
- **TuGraph**: 高性能图数据库 (Web 端口: 8888)

## 部署步骤

### 1. 准备环境
确保您的机器已安装 `Docker` 和 `Docker Compose`。

### 2. 初始化与配置
1. **复制配置**:
   ```bash
   cp .env.full.example .env
   ```
2. **填写 API Key**: 打开 `.env` 文件，完善模型密钥信息。
3. **数据库初始化**: 
   - **MySQL**: 镜像启动时会自动执行 `init/init.sql` 进行初始化。
   - **TuGraph**: 启动后需登录 Web 界面进行初步设置（详见下方“TuGraph 设置”）。

### 3. 一键启动
运行以下命令拉取镜像并启动全栈服务：
```bash
docker compose -f docker-compose.full.yml pull
docker compose -f docker-compose.full.yml up -d
```

### 4. 访问服务
- **Web 界面**: [http://localhost:8880](http://localhost:8880)
- **后端 API**: [http://localhost:5670](http://localhost:5670)
- **TuGraph 视图**: [http://localhost:8888](http://localhost:8888)

## TuGraph 设置
1. 访问 [http://localhost:8888](http://localhost:8888)。
2. 默认账号：`admin`，默认密码：`73@TuGraph`。
3. 系统会自动连接。如果需要使用 Knowledge Graph 功能，请确保在 Web UI 中已建立对应的图空间（系统通常会尝试自动连接默认空间）。

## 目录结构
- `configs/`: 包含自定义的 DB-GPT 配置文件。
- `init/`: 包含 MySQL 初始化脚本 `init.sql`。
- `data/`, `mysql_data/`, `tugraph_data/`: 用于持久化存储数据（会自动创建）。
- `logs/`: 存储运行日志。

## 注意事项
- 所有的 Docker 镜像已托管在阿里云公有仓库 (`hs_public` 命名空间)，**无需执行 docker login 即可直接拉取**。
- 第一次启动可能需要 1-2 分钟进行数据库初始化。
