# NFR-DFX-Quality-Toolkit

[**中文版**](./README-zh.md)

[**相关概念**](./Concept.md)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Project Status](https://img.shields.io/badge/status-active-success.svg)](https://github.com/turtacn/NFR-DFX-Quality-Toolkit/)

An open-source toolkit for architects and developers to systematically build high-quality software by integrating Non-Functional Requirements (NFR) with Design for Excellence (DFX) methodologies.

## The Challenge: From Abstract Qualities to Concrete Architectures

In modern software engineering, functional requirements are just the tip of the iceberg. The true determinants of a product's success—**performance, reliability, security, maintainability**—are its quality attributes. However, teams often struggle with:

-   **Vague NFRs**: Translating abstract goals like "high availability" into verifiable engineering metrics.
-   **Siloed DFX Knowledge**: DFX (Design for Excellence) principles like Design for Testability (DFT) or Reliability (DFR) remain theoretical and are not systematically embedded into the architecture.
-   **Repetitive Work**: Reinventing the wheel for common quality concerns like observability, resilience, and security in every new project.

## The Solution: NFR-DFX-Quality-Toolkit

This toolkit provides a structured, one-stop solution to bridge the gap between quality requirements and implementation. It offers:

-   **Systematic Guidance**: A comprehensive documentation hub that classifies NFRs, maps them to concrete DFX strategies, and provides architectural blueprints.
-   **Reusable Assets**: Production-ready SDKs, framework templates, and tools to accelerate development without compromising quality.
-   **Practical Examples**: Real-world case studies (e.g., e-commerce flash sales, financial core systems) demonstrating how to apply these principles in practice.
-   **Community-Driven Best Practices**: A collaborative platform for sharing and refining quality-centric architectural patterns.

## Key Features

-   **📚 Comprehensive Docs**: In-depth guides on 10+ NFRs and their mapping to DFX principles (DFT, DFR, DFS, etc.).
-   **🧩 Modular SDKs (Go)**: Lightweight, pluggable modules for:
    -   **Observability**: OpenTelemetry-based logging and distributed tracing.
    -   **Resilience**: Circuit breakers and rate limiters (Resilience4j/Sentinel patterns).
    -   **Security**: JWT/OAuth2 helpers and data encryption utilities.
    -   **Configuration**: Unified configuration management patterns.
-   **🚀 Framework Templates**: Boilerplates for kickstarting high-quality microservices:
    -   Go (Gin/Gonic)
    -   Java (Spring Boot)
    -   Node.js (NestJS)
-   **🛠️ Scaffolding & Tooling**:
    -   A CLI tool to generate new projects from our best-practice templates.
    -   CI/CD pipeline examples (GitHub Actions, GitLab CI).
    -   Optimized Dockerfiles and Kubernetes manifests.
    -   Performance (JMeter) and Chaos (Chaos Mesh) testing scripts.

### Quick Look: Code Snippet (Go SDK)

Here's a glimpse of how our observability SDK simplifies tracing:

```go
package main

import (
    "[github.com/gin-gonic/gin](https://github.com/gin-gonic/gin)"
    "[github.com/turtacn/NFR-DFX-Quality-Toolkit/pkg/sdk/observability/tracing](https://github.com/turtacn/NFR-DFX-Quality-Toolkit/pkg/sdk/observability/tracing)"
)

func main() {
    // Auto-initialize tracer based on environment variables
    shutdown, err := tracing.InitTracer("ecommerce-service")
    if err != nil {
        // Handle error
    }
    defer shutdown()

    r := gin.New()
    
    // Add the tracing middleware to automatically trace all incoming requests
    r.Use(tracing.Middleware())

    r.GET("/products/:id", func(c *gin.Context) {
        // The trace context is automatically propagated.
        // You can create child spans for more detailed tracing.
        _, span := tracing.StartSpanFromContext(c.Request.Context(), "database.query")
        defer span.End()

        // ... your logic to fetch product ...

        c.JSON(200, gin.H{"id": c.Param("id"), "name": "Awesome Gadget"})
    })

    r.Run(":8080")
}
````

## Architecture Overview

The toolkit is designed with a modular and layered architecture, ensuring that each component is decoupled and easy to use or replace. It primarily consists of documentation, reusable SDKs, framework templates, and executable tools.

For a detailed breakdown, please see our [**Architecture Document**](./docs/architecture.md).

## Getting Started

1.  **Scaffold a new project using our CLI:**

    ```bash
    # (Coming Soon)
    go install https://github.com/turtacn/NFR-DFX-Quality-Toolkit/cmd/nfr-toolkit@latest
    nfr-toolkit init my-new-service --template go-gin
    ```

2.  **Explore the documentation and examples:**

      - Dive into `docs/` to understand the NFR/DFX mapping.
      - Run the projects in `examples/` to see the concepts in action.

## Contribution

We welcome contributions\! Please read our [**Contribution Guide**](./CONTRIBUTING.md) to get started. You can check the [issues page](https://github.com/turtacn/NFR-DFX-Quality-Toolkit/issues) for ideas.

## License

This project is licensed under the MIT License. See the [LICENSE](./LICENSE) file for details.