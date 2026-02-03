# Nacos CLI

A powerful command-line tool for managing Nacos configuration center and AI skills, written in Go.

## Features

- 🚀 Fast and lightweight - single binary with no dependencies
- 💻 Interactive terminal mode with auto-completion
- 🎯 Skill management - upload, download, list, and sync AI skills
- 📝 Configuration management - list and get configurations
- 🔄 Real-time skill synchronization with Nacos
- 🌐 Namespace support for multi-environment management
- 📦 Batch operations - upload all skills at once

## Installation

### Download Binary

Download the latest release from [GitHub Releases](https://github.com/yourusername/nacos-cli/releases).

### Build from Source

```bash
# Clone the repository
git clone https://github.com/yourusername/nacos-cli.git
cd nacos-cli

# Build
go build -o nacos-cli

# Or use make
make build
```

## Quick Start

### CLI Mode

Run commands directly:

```bash
# List all skills
nacos-cli skill-list -s 127.0.0.1:8848 -u nacos -p nacos

# Get a skill
nacos-cli skill-get skill-creator -s 127.0.0.1:8848 -u nacos -p nacos

# Upload a skill
nacos-cli skill-upload /path/to/skill -s 127.0.0.1:8848 -u nacos -p nacos
```

### Interactive Terminal Mode

Start an interactive session:

```bash
nacos-cli -s 127.0.0.1:8848 -u nacos -p nacos
```

Once in terminal mode, you can run commands interactively:

```
nacos> skill-list
nacos> skill-get skill-creator
nacos> config-list
nacos> help
```

## Commands

### Skill Management

#### List Skills

```bash
# CLI mode
nacos-cli skill-list -s 127.0.0.1:8848 -u nacos -p nacos

# With filters
nacos-cli skill-list --name skill-creator --page 1 --size 20

# Terminal mode
nacos> skill-list
nacos> skill-list --name skill-creator --page 2
```

#### Get/Download Skill

Download a skill to local directory (default: `~/.skills`):

```bash
# CLI mode
nacos-cli skill-get skill-creator -s 127.0.0.1:8848 -u nacos -p nacos
nacos-cli skill-get skill-creator -o /custom/path

# Terminal mode
nacos> skill-get skill-creator
```

#### Upload Skill

Upload a skill from local directory:

```bash
# Upload single skill
nacos-cli skill-upload /path/to/skill -s 127.0.0.1:8848 -u nacos -p nacos

# Upload all skills in a directory
nacos-cli skill-upload --all /path/to/skills/folder

# Terminal mode
nacos> skill-upload /path/to/skill
nacos> skill-upload --all /path/to/skills
```

#### Sync Skill

Real-time synchronization - automatically syncs local skills when they change in Nacos:

```bash
# Sync single skill (CLI mode only)
nacos-cli skill-sync skill-creator -s 127.0.0.1:8848 -u nacos -p nacos

# Sync multiple skills
nacos-cli skill-sync skill-creator skill-analyzer

# Sync all skills
nacos-cli skill-sync --all

# Press Ctrl+C to stop synchronization
```

**Note**: `skill-sync` is only available in CLI mode, not in terminal mode.

### Configuration Management

#### List Configurations

```bash
# CLI mode
nacos-cli config-list -s 127.0.0.1:8848 -u nacos -p nacos

# With filters
nacos-cli config-list --data-id myconfig --group DEFAULT_GROUP

# With pagination
nacos-cli config-list --page 1 --size 20

# Terminal mode
nacos> config-list
nacos> config-list --data-id myconfig --page 2
```

#### Get Configuration

```bash
# CLI mode
nacos-cli config-get myconfig DEFAULT_GROUP -s 127.0.0.1:8848 -u nacos -p nacos

# Terminal mode
nacos> config-get myconfig DEFAULT_GROUP
```

### Terminal Commands

When in interactive terminal mode:

```bash
nacos> help           # Show all available commands
nacos> server         # Show server information
nacos> ns             # Show current namespace
nacos> ns production  # Switch to production namespace
nacos> clear          # Clear screen
nacos> quit           # Exit terminal
```

## Global Flags

| Flag | Short | Default | Description |
|------|-------|---------|-------------|
| --server | -s | 127.0.0.1:8848 | Nacos server address |
| --username | -u | nacos | Nacos username |
| --password | -p | nacos | Nacos password |
| --namespace | -n | (empty/public) | Nacos namespace ID |
| --help | -h | | Show help information |

## Project Structure

```
nacos-cli/
├── cmd/                  # CLI commands
│   ├── root.go          # Root command
│   ├── list_skill.go    # skill-list command  
│   ├── get_skill.go     # skill-get command
│   ├── upload_skill.go  # skill-upload command
│   ├── sync_skill.go    # skill-sync command
│   ├── list_config.go   # config-list command
│   ├── get_config.go    # config-get command
│   └── interactive.go   # Interactive terminal
├── internal/
│   ├── client/          # Nacos client
│   ├── skill/           # Skill service
│   ├── sync/            # Sync service
│   ├── listener/        # Config listener
│   ├── terminal/        # Terminal implementation
│   └── help/            # Help system
├── main.go
├── go.mod
└── README.md
```

## Development

### Prerequisites

- Go 1.21 or higher
- Nacos server (2.x recommended)

### Build

```bash
# Build binary
make build

# Or manually
go build -o nacos-cli
```

### Run Tests

```bash
# Run test script
./test.sh

# Or test specific commands
go run main.go skill-list -s 127.0.0.1:8848 -u nacos -p nacos
```

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

MIT License

## Changelog

### v0.2.0 (2026-01-28)

- Rewritten in Go for better performance and portability
- Added skill management commands (list, get, upload, sync)
- Added real-time skill synchronization with Nacos
- Added interactive terminal mode with auto-completion
- Added batch upload support for multiple skills
- Added configuration management commands
- Improved error handling and user experience
- Removed all emoji clutter from terminal output

### v0.1.0 (2026-01-27)

- Initial Python version release
- Basic configuration management
- Basic service discovery
=======
一个功能强大的 Nacos 命令行工具，支持快速连接、管理和操作 Nacos 配置中心和服务注册中心。

## 特性

- 🚀 快速安装和启动
- 🪶 **轻量级设计** - 无需重量级 SDK，仅使用标准 HTTP 请求
- 💻 交互式终端界面
- 🎨 美观的彩色输出和语法高亮
- 📝 支持配置管理（查看、发布、删除）
- 🔍 支持服务发现和查询
- ⚙️ 灵活的连接参数配置

## 安装

### 从源码安装

```bash
# 克隆仓库
git clone https://github.com/yourusername/nacos-cli.git
cd nacos-cli

# 安装依赖
pip install -r requirements.txt

# 安装到系统
pip install -e .
```

### 使用 pip 安装（待发布）

```bash
pip install nacos-cli
```

## 快速开始

### 连接到本地 Nacos

默认连接到 `127.0.0.1:8848`：

```bash
nacos-cli
```

### 连接到远程 Nacos

```bash
nacos-cli --host 192.168.1.100 --port 8848
```

或使用简写：

```bash
nacos-cli -h 192.168.1.100 -p 8848
```

### 指定用户名和密码

```bash
nacos-cli -h 192.168.1.100 -p 8848 -u admin -pw admin123
```

### 指定命名空间

```bash
nacos-cli -h 192.168.1.100 -p 8848 -n your-namespace-id
```

## 使用指南

连接成功后，会进入交互式终端，支持以下命令：

### 配置管理

#### 列出所有配置

```bash
nacos> list
# 或
nacos> ls
```

#### 获取配置内容

```bash
nacos> get <dataId> [group]

# 示例
nacos> get myconfig
nacos> get myconfig DEFAULT_GROUP
```

#### 发布/更新配置

```bash
nacos> set <dataId> <group> <content>

# 示例
nacos> set myconfig DEFAULT_GROUP 'server.port=8080'
nacos> set app.yml DEFAULT_GROUP 'key: value'
```

#### 删除配置

```bash
nacos> delete <dataId> [group]
# 或
nacos> rm <dataId> [group]

# 示例
nacos> delete myconfig
nacos> rm myconfig DEFAULT_GROUP
```

### 服务管理

#### 列出所有服务

```bash
nacos> services
# 或
nacos> svc
```

#### 查看服务详情

```bash
nacos> service <serviceName> [group]
# 或
nacos> detail <serviceName> [group]

# 示例
nacos> service myservice
nacos> detail myservice DEFAULT_GROUP
```

### 其他命令

```bash
nacos> help        # 显示帮助信息
nacos> clear       # 清空屏幕
nacos> exit        # 退出终端
```

## 命令行参数

| 参数 | 简写 | 默认值 | 说明 |
|------|------|--------|------|
| --host | -h | 127.0.0.1 | Nacos 服务器地址 |
| --port | -p | 8848 | Nacos 服务器端口 |
| --username | -u | nacos | Nacos 用户名 |
| --password | -pw | nacos | Nacos 密码 |
| --namespace | -n | (空) | Nacos 命名空间 ID |
| --version | | | 显示版本信息 |
| --help | | | 显示帮助信息 |

## 依赖

- Python 3.8+
- click - 命令行参数解析
- rich - 美化终端输出
- prompt-toolkit - 交互式终端
- requests - HTTP 请求

**注意**：本项目使用纯 HTTP REST API 与 Nacos 通信，不依赖官方 SDK，更加轻量。

## 开发

### 安装开发环境

```bash
git clone https://github.com/yourusername/nacos-cli.git
cd nacos-cli
pip install -r requirements.txt
pip install -e .
```

### 运行

```bash
python -m nacos_cli.main
```

## 贡献

欢迎提交 Issue 和 Pull Request！

## 许可证

MIT License

## 作者

Your Name

## 更新日志

### v0.1.0 (2026-01-27)

- ✨ 初始版本发布
- 支持基本的配置管理功能
- 支持服务查询功能
- 交互式终端界面
- 语法高亮显示
