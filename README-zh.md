# NFR-DFX-Quality-Toolkit 开源项目

[**English Version**](./README.md)

[**Concept**](./Concept.md)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Project Status](https://img.shields.io/badge/status-active-success.svg)](https://github.com/turtacn/NFR-DFX-Quality-Toolkit/)

一个面向架构师和开发者的开源工具包，旨在通过系统性地融合非功能性需求（NFR）与卓越设计（DFX）方法论，构建高质量的软件。

## 核心挑战：从抽象质量到具体架构

在现代软件工程中，功能需求只是冰山一角。真正决定产品成败的，是其**性能、可靠性、安全性、可维护性**等质量属性。然而，团队常常面临以下困境：

-   **模糊的NFR**：难以将“高可用”这类抽象目标，转化为可验证的工程指标。
-   **孤立的DFX知识**：DFX（Design for Excellence）原则，如可测试性设计（DFT）或可靠性设计（DFR），停留在理论层面，未能系统性地融入架构。
-   **重复性工作**：在每个新项目中，都需要为可观测性、弹性、安全等通用质量问题重复造轮子。

## 解决方案：NFR-DFX-Quality-Toolkit

本工具包提供了一个结构化的一站式解决方案，旨在弥合质量需求与工程实现之间的鸿沟。它提供：

-   **体系化指南**：一个全面的文档中心，对NFR进行分类，将其映射到具体的DFX策略，并提供架构蓝图。
-   **可复用资产**：生产级的SDK、框架模板和工具集，在不牺牲质量的前提下加速开发。
-   **实践性示例**：源于真实世界的案例研究（如电商秒杀、金融核心），展示如何在实践中应用这些原则。
-   **社区驱动的最佳实践**：一个协作平台，用于分享和迭代以质量为中心的架构模式。

## 主要功能特性

-   **📚 完备的文档**：深入介绍10种以上的NFR，及其与DFX原则（DFT、DFR、DFS等）的映射关系。
-   **🧩 模块化SDK (Go)**：轻量级、可插拔的模块，用于：
    -   **可观测性**：基于OpenTelemetry的日志与分布式追踪。
    -   **弹性**：熔断、限流等（参考Resilience4j/Sentinel模式）。
    -   **安全性**：JWT/OAuth2辅助工具与数据加密库。
    -   **配置管理**：统一的配置管理模式。
-   **🚀 框架模板**：用于快速启动高质量微服务的项目骨架：
    -   Go (Gin/Gonic)
    -   Java (Spring Boot)
    -   Node.js (NestJS)
-   **🛠️ 脚手架与工具链**：
    -   一个CLI工具，可基于我们的最佳实践模板生成新项目。
    -   CI/CD流水线示例 (GitHub Actions, GitLab CI)。
    -   优化后的Dockerfile和Kubernetes清单文件。
    -   性能测试 (JMeter) 与混沌工程 (Chaos Mesh) 脚本。

### 代码速览 (Go SDK)

一窥我们的可观测性SDK如何简化链路追踪：

```go
package main

import (
    "github.com/gin-gonic/gin"
    "github.com/turtacn/NFR-DFX-Quality-Toolkit/pkg/sdk/observability/tracing"
)

func main() {
    // 基于环境变量自动初始化Tracer
    shutdown, err := tracing.InitTracer("ecommerce-service")
    if err != nil {
        // 错误处理
    }
    defer shutdown()

    r := gin.New()
    
    // 添加追踪中间件，自动追踪所有入口请求
    r.Use(tracing.Middleware())

    r.GET("/products/:id", func(c *gin.Context) {
        // 追踪上下文被自动传递
        // 你可以创建子Span以实现更精细的追踪
        _, span := tracing.StartSpanFromContext(c.Request.Context(), "database.query")
        defer span.End()

        // ... 你的业务逻辑 ...

        c.JSON(200, gin.H{"id": c.Param("id"), "name": "一个很棒的商品"})
    })

    r.Run(":8080")
}
````

## 架构概览

本工具包采用模块化、分层化的架构设计，确保各组件松耦合且易于使用或替换。它主要由文档、可复用SDK、框架模板和可执行工具组成。

欲了解详细设计，请参阅我们的[**架构设计文档**](./docs/architecture.md)。

## 快速开始

1.  **使用我们的CLI工具生成一个新项目：**

    ```bash
    # (即将推出)
    go install https://github.com/turtacn/NFR-DFX-Quality-Toolkit/cmd/nfr-toolkit@latest
    nfr-toolkit init my-new-service --template go-gin
    ```

2.  **浏览文档和示例项目：**

      - 深入 `docs/` 目录，理解NFR与DFX的映射关系。
      - 运行 `examples/` 中的项目，观摩这些概念的实际应用。

## 如何贡献

我们欢迎任何形式的贡献！请阅读我们的[**贡献指南**](https://www.google.com/search?q=./CONTRIBUTING.md)来开始。您可以查看 [Issues页面](https://github.com/turtacn/NFR-DFX-Quality-Toolkit/issues)来寻找灵感。

## 许可证

本项目基于 MIT 许可证。详情请参阅 [LICENSE](./LICENSE) 文件。