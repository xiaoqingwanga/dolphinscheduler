# Apache DolphinScheduler Directory Structure

This document provides a comprehensive overview of the Apache DolphinScheduler project directory structure and explains what each component contains.

## Overview

Apache DolphinScheduler is a distributed, easy-to-expand visual DAG workflow scheduling system. The project follows a modular, plugin-based architecture that allows for high extensibility and customization.

## Core Server Components

### `dolphinscheduler-master`
The master server implementation that manages workflow execution, task scheduling, and coordination. The master handles:
- Workflow definition management
- Task dependency resolution
- Task distribution to workers
- DAG execution orchestration
- High availability coordination

### `dolphinscheduler-worker`
The worker server implementation that executes tasks assigned by the master. Workers handle:
- Actual task execution (Shell, SQL, Spark, etc.)
- Task status reporting
- Resource management
- Log collection and reporting

### `dolphinscheduler-api`
The REST API server that provides HTTP endpoints for the UI and external clients. Handles:
- User authentication and authorization
- Project management
- Workflow definition CRUD operations
- Monitoring and metrics endpoints
- System administration APIs

### `dolphinscheduler-ui`
Frontend web interface built with Vue.js/Vite. Provides the user dashboard for:
- Creating and managing workflows
- Monitoring execution status
- Managing data sources
- System administration
- User and tenant management

## Plugin Architecture

### `dolphinscheduler-task-plugin`
Contains 30+ task type implementations organized by category:

**Data Processing:**
- Spark, Flink, MapReduce
- Python, Java, Shell
- Zeppelin, Jupyter

**Database:**
- SQL, Procedure, HiveCLI
- ClickHouse, Doris

**Data Integration:**
- DataX, Seatunnel, Sqoop, Chunjun
- Dinky, Linkis

**Machine Learning:**
- MLflow, PyTorch, TensorFlow
- AWS Sagemaker, Aliyun Serverless Spark

**Communication:**
- HTTP, gRPC, WebSocket
- Email, DingTalk, Slack

**Cloud Services:**
- AWS, Azure, Google Cloud
- Alibaba Cloud, Tencent Cloud

### `dolphinscheduler-datasource-plugin`
Database connection plugins for 25+ data sources:

**Relational Databases:**
- MySQL, PostgreSQL, Oracle
- SQL Server, DB2, H2

**Big Data Platforms:**
- Hive, ClickHouse, Doris
- StarRocks, Trino, Presto

**Cloud Data Warehouses:**
- Snowflake, Redshift, Athena
- Azure SQL, BigQuery

**Chinese Databases:**
- Dameng, OceanBase, DolphinDB
- TiDB, KingBase

**In-Memory & Search:**
- Redis, Elasticsearch
- Phoenix, HBase

### `dolphinscheduler-storage-plugin`
Storage backend plugins for different file systems:
- **HDFS**: Hadoop Distributed File System
- **S3**: Amazon Simple Storage Service
- **ABS**: Azure Blob Storage
- **GCS**: Google Cloud Storage
- **OSS**: Alibaba Cloud Object Storage Service
- **COS**: Tencent Cloud Object Storage
- **OBS**: Huawei Cloud Object Storage Service

### `dolphinscheduler-registry`
Service discovery and coordination plugins:
- **Zookeeper**: Default coordination service
- **Etcd**: Distributed key-value store
- **MySQL/JDBC**: Database-based registry
- Handles master/worker node discovery, load balancing, and distributed locking

### `dolphinscheduler-dao-plugin`
Database access layer plugins:
- **MySQL**: MySQL/MariaDB support
- **PostgreSQL**: PostgreSQL support
- **H2**: In-memory database for testing
- Provides database abstraction for metadata storage

## Supporting Components

### `dolphinscheduler-alert`
Alert and notification system for:
- Workflow failure notifications
- Task status updates
- Custom alert rules
- Multiple notification channels (Email, Slack, DingTalk, etc.)

### `dolphinscheduler-service`
Core business logic services shared across components:
- Workflow definition services
- Task execution services
- User management services
- Project management services

### `dolphinscheduler-common`
Shared utilities, constants, and common code:
- Enumerations and constants
- Utility classes
- Common data structures
- Configuration management

### `dolphinscheduler-spi`
Service Provider Interfaces defining plugin contracts:
- Task plugin interfaces
- DataSource plugin interfaces
- Storage plugin interfaces
- Registry plugin interfaces

### `dolphinscheduler-bom`
Bill of Materials for Maven dependency management:
- Centralized version management
- Dependency consistency across modules
- Build configuration

## Development & Operations

### `deploy`
Deployment configurations and scripts:

**Docker:**
- Dockerfiles for all components
- Docker Compose configurations
- Container orchestration

**Kubernetes:**
- Kubernetes manifests
- Helm charts
- K8s operator configurations

**Terraform:**
- Infrastructure as Code templates
- Cloud deployment automation
- Environment provisioning

### `script`
Shell scripts for system management:
- `dolphinscheduler-daemon.sh`: Service management script
- `install-plugins.sh`: Plugin installation utility
- Environment configuration files
- Startup and shutdown scripts

### `docs`
Project documentation and guides:
- User guides
- Developer documentation
- API documentation
- Deployment guides
- Architecture documentation

### `tools`
Development tools and utilities:
- Build tools
- Testing utilities
- Code generation tools
- Migration scripts

### `config`
Configuration templates and examples:
- Application properties
- Database configurations
- Logging configurations
- Security settings

### `dolphinscheduler-dist`
Build and packaging configuration:
- Maven assembly configurations
- Distribution packaging
- Release automation
- Version management

### `dolphinscheduler-e2e`
End-to-end integration tests:
- Workflow execution tests
- API integration tests
- Performance tests
- Compatibility tests

### `dolphinscheduler-standalone-server`
Standalone deployment mode:
- All-in-one deployment
- Embedded database
- Simplified configuration
- Development and testing

## Specialized Modules

### `dolphinscheduler-authentication`
Security and authentication mechanisms:
- JWT token management
- Password encryption
- User session management
- Integration with external auth systems

### `dolphinscheduler-eventbus`
Event-driven communication system:
- Message publishing and subscription
- Event routing
- Asynchronous communication
- Event persistence

### `dolphinscheduler-extract`
Data extraction and processing utilities:
- ETL operations
- Data transformation
- Format conversion
- Validation utilities

### `dolphinscheduler-meter`
Metrics collection and monitoring:
- Performance metrics
- Resource usage monitoring
- Custom metrics collection
- Integration with monitoring systems

### `dolphinscheduler-scheduler-plugin`
Custom scheduling algorithms and strategies:
- Cron-based scheduling
- Priority scheduling
- Resource-aware scheduling
- Custom scheduling policies

### `dolphinscheduler-task-executor`
Task execution engine and runtime:
- Task lifecycle management
- Resource allocation
- Execution context management
- Error handling and recovery

### `dolphinscheduler-yarn-aop`
Yarn integration aspects:
- Hadoop Yarn resource management
- Container allocation
- Application lifecycle management

### `dolphinscheduler-tools`
Administrative and maintenance tools:
- Database migration tools
- Configuration validation
- System diagnostics
- Performance analysis

## Project Structure Files

### Root Configuration Files
- `.asf.yaml`: Apache Software Foundation project configuration
- `pom.xml`: Maven parent project configuration
- `LICENSE`: Project license
- `NOTICE`: Legal notices and attributions

### Development Tools
- `.gitignore`: Git ignore patterns
- `.pre-commit-config.yaml`: Pre-commit hooks configuration
- `.licenserc.yaml`: License header configuration
- `lombok.config`: Lombok configuration

### Documentation
- `README.md`: Project overview and getting started
- `README_zh_CN.md`: Chinese documentation
- `CONTRIBUTING.md`: Contribution guidelines

### Media
- `images/`: UI screenshots, project logos, and documentation images

## Architecture Benefits

This modular architecture provides several key benefits:

1. **Extensibility**: Plugin-based design allows easy addition of new task types, data sources, and storage systems

2. **Flexibility**: Multiple deployment options (standalone, cluster, containerized, cloud-native)

3. **Scalability**: Distributed architecture supports horizontal scaling of master and worker nodes

4. **Maintainability**: Clear separation of concerns with well-defined module boundaries

5. **Customization**: Rich plugin ecosystem supports various enterprise requirements

6. **Compatibility**: Multi-database, multi-storage, and multi-cloud support for diverse environments

## Getting Started

To explore the codebase:

1. Start with `dolphinscheduler-api` to understand the REST API structure
2. Review `dolphinscheduler-master` and `dolphinscheduler-worker` for core scheduling logic
3. Explore `dolphinscheduler-task-plugin` for available task types
4. Check `dolphinscheduler-ui` for frontend implementation
5. Refer to `docs/` for detailed documentation and guides

For development guidelines, see `CONTRIBUTING.md` and the developer documentation in `docs/`.