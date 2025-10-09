# 瞬刻 - *更简洁、更现代化的内容发布平台*

使用vercle快速部署：[<img src="https://vercel.com/button" alt="Deploy on Vercel" height="30">](https://vercel.com/new/clone?repository-url=https://github.com/reaishijie/moments&root-directory=frontend&env=VITE_API_BASE_URL&project-name=moments&repository-name=moments)

## 项目概述

瞬刻是一个现代化的社交媒体应用，专注于为用户提供简洁、流畅的内容分享体验。项目采用前后端分离架构，支持文字、图片、视频等多种内容类型的发布和交互。

### 项目特色

- 🚀 **现代化技术栈**: Vue 3 + Node.js + TypeScript + MySQL
- 📱 **移动端优先**: 响应式设计，完美适配移动设备
- 🔐 **完善的认证系统**: JWT 认证，支持游客访问和点赞
- 💬 **多级评论系统**: 支持评论发表与回复
- 📍 **位置服务**: 获取基础地理位置功能
- 📊 **完整的日志系统**: 用户行为追踪和系统监控

## 快速部署请查看：[doc/quickDeploy.md](doc/quickDeploy-readme.md)

使用`build.sh`时候注意前端`.env`的接口修改为 `VITE_API_BASE_URL=/api` ，前后端分离则使用 `VITE_API_BASE_URL=http://localhost:9889/api`(记得替换成你真实后端地址)

## 项目预览


|                                                    首页（亮）                                                    |                                                    首页（暗）                                                    |                                                     文章详情                                                     |
| :---------------------------------------------------------------------------------------------------------------: | :---------------------------------------------------------------------------------------------------------------: | :---------------------------------------------------------------------------------------------------------------: |
| <img width="300" alt="1" src="https://github.com/user-attachments/assets/25231327-80e1-426f-9afd-6a1bf3fce939" /> | <img width="300" alt="2" src="https://github.com/user-attachments/assets/3ac8fdd8-46f7-4a17-bdfd-080737268c37" /> | <img width="300" alt="3" src="https://github.com/user-attachments/assets/ca4ff306-5aec-4ec9-b06c-e8fb833fa8d6" /> |
|                                                     **推广**                                                     |                                                  **发布文章**                                                  |                                                   **用户资料**                                                   |
| <img width="300" alt="4" src="https://github.com/user-attachments/assets/01710755-98d4-4b43-85b7-1b08a675fa27" /> | <img width="300" alt="5" src="https://github.com/user-attachments/assets/45735944-d30d-4f9e-b05d-1c3017b0774f" /> | <img width="300" alt="6" src="https://github.com/user-attachments/assets/b946afd9-3451-4175-a65a-20647e104b1d" /> |

## 更新计划：[doc/update.md](doc/update.md)

### 本次更新

* [X]  视频封面（首帧图）
* [X]  广告类型跳转超链接
* [X]  友情链接页面
* [X]  前端通知：数据库表
* [X]  后台上传文件接口：新增本地上传和S3储存桶（我是使用CF R2进行的测试没问题）
* [X]  文章标签（TAG）：数据库
* [X]  全局黑暗模式 + 回到顶部

## 程序开发

```bash
# 1. 克隆项目
git clone https://github.com/reaishijie/moments.git
cd moments

# 2. 后端环境搭建
cd backend
npm install

# 创建环境配置文件
cp .env.example .env
# 编辑 .env 文件，配置数据库连接和其他环境变量

# 数据库初始化
npx prisma migrate deploy
npx prisma generate
npm run db:setup

# 启动后端服务
npm run dev

# 3. 前端环境搭建（新终端窗口）
cd ../frontend
npm install

# 创建环境配置文件
cp .env.example .env
# 编辑 .env 文件，配置 API 地址等

# 启动前端服务
npm run dev
```

## 程序上线

### 软件环境安装

- Node.JS环境（16+）
- MySQL（5.6+）
- PM2（用于持久化）

### 程序运行

```bash
 # 1. 克隆项目
git clone https://github.com/reaishijie/moments.git
cd moments

# 2. 后端环境搭建
cd backend
npm install

# 创建环境配置文件
cp .env.example .env
# 编辑 .env 文件，配置数据库连接和其他环境变量

# 数据库初始化
npx prisma migrate deploy
npx prisma generate
npm run db:setup

# 构建后端文件目录
npm run build

# 使用pm2 持久化后端服务
pm2 start dist/index.js


# 3. 前端环境搭建（新终端窗口）
cd ../frontend
npm install

# 创建环境配置文件
cp .env.example .env
# 编辑 .env 文件，配置 API 地址等

# 构建前端文件目录
npm run build

# 启动前端服务
# 在nginx/OpenResty添加网站，目录选择frontend/dist
#伪静态规则： 
location / {
    try_files $uri $uri/ /index.html;
 }
```

## 开源协议

本项目采用 Apache 开源协议，详见 [LICENSE](LICENSE) 文件。

## 致谢

感谢所有为本项目做出贡献的开发者和用户！

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=reaishijie/moments&type=Date)](https://www.star-history.com/#reaishijie/moments&Date)
