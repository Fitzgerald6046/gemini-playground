# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview
This is a Gemini 2.0 multimodal chat playground that can be deployed on Deno or Cloudflare Workers. It provides a web interface for interacting with Gemini AI models with support for text, audio, video, and screen sharing. The project also includes an API proxy that converts Gemini API calls to OpenAI-compatible format.

## Commands

### Development
- **Start Deno development server**: `deno run --allow-net --allow-read src/deno_index.ts`
- **Start Deno via task**: `deno task start`
- **Start Cloudflare Workers development**: `wrangler dev` or `npm run dev`

### Deployment
- **Deploy to Cloudflare Workers**: `wrangler deploy` or `npm run deploy`

### Testing
- **Run tests**: `npm test` or `vitest`

## Architecture

### Deployment Targets
The project supports two deployment environments:
1. **Deno**: Entry point at `src/deno_index.ts` - handles static file serving and WebSocket proxying
2. **Cloudflare Workers**: Entry point at `src/index.js` - uses Workers runtime with KV storage for static assets

### Core Components

#### API Proxy (`src/api_proxy/worker.mjs`)
- Converts Gemini API to OpenAI-compatible format
- Handles `/v1/chat/completions`, `/v1/embeddings`, and `/v1/models` endpoints
- Supports streaming responses and various content types (text, images, audio)
- Based on the openai-gemini project by PublicAffairs

#### WebSocket Proxy
- Proxies WebSocket connections to Gemini's generative language API
- Handles real-time bidirectional communication for multimodal interactions
- Manages connection lifecycle and message queuing

#### Frontend (`src/static/`)
- **Main application**: `js/main.js` - coordinates UI, audio, video, and WebSocket interactions
- **WebSocket client**: `js/core/websocket-client.js` - handles Gemini API WebSocket connections
- **Audio system**: `js/audio/` - manages audio recording and streaming with worklets
- **Video system**: `js/video/` - handles camera and screen recording
- **Tools integration**: `js/tools/` - supports Google Search and weather tools
- **Configuration**: `js/config/config.js` - centralized configuration management

### Key Features
- **Multimodal input**: Text, audio, video (camera), and screen sharing
- **Real-time communication**: WebSocket-based streaming with Gemini 2.0
- **OpenAI API compatibility**: Proxy layer for integration with existing tools
- **Tool integration**: Google Search and weather tools
- **Mobile-optimized**: Responsive design for mobile devices

### Configuration
- API keys and settings are managed through the web interface
- System instructions and response types can be customized
- Audio worklets handle real-time audio processing
- Video frame rates and quality can be configured

## Development Notes
- The project uses vanilla JavaScript (no build system required)
- Audio processing uses Web Audio API with custom worklets
- Video capture utilizes MediaRecorder API and Canvas for frame extraction
- WebSocket connections are proxied through the server to avoid CORS issues
- The API proxy handles content transformation between OpenAI and Gemini formats
CLAUDE.md

此文件提供了在此存储库中使用代码时对Claude Code（claude.ai/code）的指导。
项目概述

这是一个Gemini 2.0多模态聊天实验平台，可以部署在Deno或Cloudflare Workers上。它提供了一个Web界面，用于与Gemini AI模型进行交互，支持文本、音频、视频和屏幕共享。该项目还包括一个API代理，将Gemini API调用转换为与OpenAI兼容的格式。
命令

开发

启动Deno开发服务器: deno run --allow-net --allow-read src/deno_index.ts
通过任务启动Deno: deno task start
启动Cloudflare Workers开发: wrangler dev 或 npm run dev

部署

部署到Cloudflare Workers: wrangler deploy 或 npm run deploy

测试

运行测试: npm test 或 vitest

架构

部署目标

该项目支持两种部署环境：
Deno: 入口文件为src/deno_index.ts - 负责静态文件服务和WebSocket代理
Cloudflare Workers: 入口文件为src/index.js - 使用Workers运行时，结合KV存储静态资产

核心组件

API代理 (src/api_proxy/worker.mjs)

将Gemini API转换为OpenAI兼容格式
处理/v1/chat/completions、/v1/embeddings和/v1/models端点
支持流式响应和多种内容类型（文本、图片、音频）
基于PublicAffairs的openai-gemini项目

WebSocket代理

将WebSocket连接代理到Gemini的生成语言API
处理多模态交互的实时双向通信
管理连接生命周期和消息队列

前端 (src/static/)

主应用: js/main.js - 协调UI、音频、视频和WebSocket交互
WebSocket客户端: js/core/websocket-client.js - 处理Gemini API的WebSocket连接
音频系统: js/audio/ - 管理音频录制和流式传输，使用音频工作单元（worklets）
视频系统: js/video/ - 处理摄像头和屏幕录制
工具集成: js/tools/ - 支持Google搜索和天气工具
配置管理: js/config/config.js - 集中式配置管理

主要功能

多模态输入: 支持文本、音频、视频（摄像头）和屏幕共享
实时通信: 基于WebSocket的流式传输，支持Gemini 2.0
OpenAI API兼容性: 代理层用于与现有工具集成
工具集成: 支持Google搜索和天气工具
移动优化: 针对移动设备的响应式设计

配置

API密钥和设置通过Web界面进行管理
系统指令和响应类型可以自定义
音频工作单元负责实时音频处理
视频帧率和质量可以配置

开发笔记

项目使用原生JavaScript（不需要构建系统）
音频处理使用Web Audio API，结合自定义工作单元（worklets）
视频捕捉使用MediaRecorder API和Canvas进行帧提取
WebSocket连接通过服务器代理，以避免CORS问题
API代理负责将内容在OpenAI和Gemini格式之间进行转换
