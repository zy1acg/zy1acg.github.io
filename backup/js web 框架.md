- Express
- Fastify
- Hono
- Elysia

维度 | Express | Fastify | Hono | Elysia
-- | -- | -- | -- | --
性能 | 基准 | 高 (约2倍于Express) | 极高 (Node.js环境媲美Fastify，边缘环境碾压) | 恐怖 (Bun环境下可达Express的21倍)
轻量级 | 较重 (572KB) | 中等 | 极致 (14KB) | 轻量
生产就绪 | 极高 (行业标准) | 高 (成熟稳定) | 中等 (生态较新，但已被大厂核心产品使用) | 中等 (生态和运行时稳定性仍在验证中)
生态/插件 | 最丰富 | 丰富且成熟 | 较新，正在快速发展 | 较新，正在快速发展
跨平台/边缘 | 仅Node.js | 仅Node.js | 完美支持 (Workers, Bun, Deno, Node.js) | 主要为Bun设计，兼容Node.js
TypeScript支持 | 需配置 | 优秀 | 优秀 (原生类型推导) | 极致 (端到端类型安全)
学习曲线 | 低 | 低 (类似Express) | 低 (API简洁) | 中等 (新概念较多)


