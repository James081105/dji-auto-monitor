# 大疆商品监控系统

## 项目简介

大疆商城商品监控系统用户用户方便快速监控到库存商品变化，支持bark推送、wxpusher以及pushplus

## 项目截图
<img width="1354" height="574" alt="ec4d97ce-d83f-424e-9b7c-964ffc3b39be" src="https://github.com/user-attachments/assets/cd27f8f1-874a-4f07-be7e-0b2476b28ec4" />
<img width="1361" height="577" alt="202efa08-15d9-4309-a1bf-ef2f82e7ccce" src="https://github.com/user-attachments/assets/386f2bc9-c6c3-4e16-9a23-4fa96e84ba1e" />
<img width="1312" height="570" alt="7d94a745-1e13-4359-87b2-aa160d33d749" src="https://github.com/user-attachments/assets/7b896388-3d90-4684-bbf4-f1d59246de07" />
<img width="1366" height="606" alt="5b307710-55ec-4a21-b775-ba10b2f8b9c1" src="https://github.com/user-attachments/assets/78611d2c-ebb6-41e0-932b-cee2149e7158" />
<img width="1362" height="597" alt="2aab3ef8-d0fe-4e1c-855d-a6fe0d47d5ac" src="https://github.com/user-attachments/assets/2c7e8e9f-2b06-46cf-bb5c-cdf09d7eb328" />
<img width="1331" height="559" alt="0fe77f23-6304-47cd-b626-e1e2c8271543" src="https://github.com/user-attachments/assets/2fd6851f-02b6-45d6-b0d9-444d0d3af2cb" />


## 联系方式

v：james_hui666
闲鱼：tb3345884683

### 目标用户
- 系统集成商
- 无人机运维团队
- 安防监控平台开发人员

## 核心功能

### 1. 数据接收
- `djipush.py`: 接收来自DJI设备或平台的数据推送

### 2. 主动查询
- `djisearch.py`: 发起搜索请求

### 3. 用户管理
- Web管理界面：基于Flask框架实现的用户友好的管理界面
- 用户授权管理：支持用户注册、授权时间管理、到期提醒等
- 多推送渠道支持：支持WxPusher和Bark推送通知

### 4. 配置管理
- `config.yaml`: 存放系统配置参数，如API地址等
- 基于YAML的配置管理，支持灵活部署

### 5. 定时任务
- 每日8点自动执行用户授权到期检查
- 支持调度器管理，可启动/停止监控任务

## 技术选型

- **后端**: Python脚本（无Web框架依赖）
- **Web管理界面**: Flask框架
- **配置文件**: YAML格式
- **通信协议**: HTTP/HTTPS

## 安装与部署

### 环境要求
- Python 3.7 或更高版本
- pip 包管理工具

### 安装步骤
1. 克隆或复制项目到本地目录
2. 安装依赖：
   ```bash
   pip install -r requirements.txt
   ```
3. 根据实际环境修改 `config.yaml` 配置文件

### 运行方式
- 启动监听：`python djipush.py`
- 执行查询：`python djisearch.py`
- 启动Web管理界面：`python web_manager.py`
- 启动调度器：`python start_scheduler.py`

## 功能特性

### 用户管理功能
1. **用户搜索**：支持按用户名、备注、注册时间、到期时间等关键词搜索
2. **用户排序**：支持按用户名、注册时间、到期时间进行升序/降序排序
3. **用户授权管理**：
   - 用户注册时自动发送通知（用户名、授权时间、到期时间、推送方式）
   - 用户授权到期前三天开始发送提醒通知
   - 每日8点自动执行用户授权检查

### 推送通知
- 支持WxPusher和Bark双渠道推送
- 用户注册通知
- 授权到期提醒
- 所有推送使用纯文本格式，不进行美化处理

### 调度器功能
- 可启动/停止监控任务
- 定时执行用户授权检查
- 实时监控状态查看

## 使用说明

### Web管理界面
默认登录账号：admin
默认登录密码：123456
支持在后台修改用户名和密码

### 配置文件
主要配置项：
- `admin`: 管理员账号密码
- `products`: 监控的商品列表
- `users`: 用户授权信息
- `wxpusher`: WxPusher推送配置
- `bark_urls`: Bark推送地址列表

### 定时任务设置
提供多种方式设置每日8点执行的用户授权检查：
1. 使用Windows任务计划程序（推荐）
2. 手动运行服务脚本
3. 集成到现有调度器中

## 安全要求
- 注意 `config.yaml` 中是否包含敏感信息（如密钥），需做好权限保护
- urllib3版本 ≥1.26.5，已规避部分已知漏洞

## 已知限制
- 无异常处理细节说明，可能存在健壮性问题
- 无单元测试或自动化测试框架集成
- 功能扩展性有限，若需接入多种设备类型，当前结构可能需重构

## 维护与支持
- 可作为后台常驻进程运行
- 建议自行添加日志记录机制
- 需保证网络可达DJI相关API服务端点
