# n8n Codebase Index

## Overview
n8n is a workflow automation platform that gives technical teams the flexibility of code with the speed of no-code. It's built as a monorepo using pnpm workspaces with TypeScript and Node.js.

**Version**: 1.100.0
**License**: Fair-code (Sustainable Use License + n8n Enterprise License)
**Node.js**: >=22.16
**Package Manager**: pnpm >=10.2.1

## Architecture Overview

n8n follows a modular monorepo architecture with clear separation of concerns:

- **Backend**: Node.js/TypeScript server with CLI, core workflow engine, and API
- **Frontend**: Vue.js 3 application with modern tooling (Vite, TypeScript)
- **Workflow Engine**: Core workflow execution and node system
- **Nodes**: 400+ integrations with external services
- **Extensions**: Plugin system and additional functionality

## Repository Structure

### Root Level Configuration
```
├── package.json              # Root monorepo configuration
├── pnpm-workspace.yaml       # Workspace definitions and catalogs
├── turbo.json               # Turborepo build orchestration
├── tsconfig.json            # Root TypeScript configuration
├── biome.jsonc              # Code formatting and linting
├── lefthook.yml             # Git hooks configuration
└── vitest.workspace.ts      # Testing configuration
```

### Main Packages

#### 1. CLI Package (`packages/cli/`)
**Main executable and server application**
- **Package**: `n8n` (v1.100.0)
- **Purpose**: Main n8n server, CLI commands, API endpoints
- **Key Features**:
  - OCLIF-based CLI interface
  - Express.js REST API server
  - Workflow execution orchestration
  - User management and authentication
  - Database management (SQLite, PostgreSQL, MySQL, MariaDB)
  - Enterprise features (SSO, permissions, etc.)

**Key Directories**:
```
src/
├── commands/           # CLI commands
├── controllers/        # API route controllers
├── databases/          # Database schemas and migrations
├── services/          # Business logic services
├── auth/              # Authentication & authorization
├── webhooks/          # Webhook handling
├── workflows/         # Workflow management
├── executions/        # Execution tracking
├── user-management/   # User & team management
├── license/           # License management
├── sso.ee/           # Enterprise SSO features
└── permissions.ee/    # Enterprise permissions
```

#### 2. Core Package (`packages/core/`)
**Core workflow execution engine**
- **Package**: `n8n-core` (v1.99.0)
- **Purpose**: Workflow execution, node communication, data processing
- **Key Features**:
  - Workflow execution engine
  - Node execution context
  - Data transformation utilities
  - HTTP request handling
  - File processing
  - Credential management

#### 3. Workflow Package (`packages/workflow/`)
**Workflow definition and validation**
- **Package**: `n8n-workflow` (v1.97.0)
- **Purpose**: Workflow schema, validation, expression evaluation
- **Key Features**:
  - Workflow data structures
  - Expression evaluation engine
  - Node type definitions
  - Data validation
  - Workflow serialization

#### 4. Nodes Base Package (`packages/nodes-base/`)
**400+ built-in integrations**
- **Package**: `n8n-nodes-base` (v1.98.0)
- **Purpose**: All built-in nodes and credentials
- **Key Features**:
  - 400+ service integrations
  - Authentication credentials for services
  - Node implementations for popular services
  - Trigger nodes for webhooks and polling

**Major Integration Categories**:
- **Communication**: Slack, Discord, Telegram, WhatsApp, Email
- **CRM**: Salesforce, HubSpot, Pipedrive, Copper
- **Cloud Storage**: Google Drive, Dropbox, AWS S3, OneDrive
- **Databases**: MySQL, PostgreSQL, MongoDB, Redis
- **AI/ML**: OpenAI, LangChain nodes
- **E-commerce**: Shopify, WooCommerce, Stripe
- **Project Management**: Jira, Asana, Trello, Monday.com
- **Marketing**: Mailchimp, SendGrid, ActiveCampaign

#### 5. Frontend Package (`packages/frontend/editor-ui/`)
**Vue.js workflow editor interface**
- **Package**: `n8n-editor-ui` (v1.100.0)
- **Purpose**: Web-based workflow editor and management interface
- **Key Technologies**:
  - Vue.js 3 with Composition API
  - TypeScript
  - Vite build system
  - Element Plus UI components
  - Vue Flow for workflow canvas
  - CodeMirror for code editing
  - Pinia for state management

### Supporting Packages (`packages/@n8n/`)

#### Core Infrastructure
- **`@n8n/config`**: Configuration management
- **`@n8n/constants`**: Shared constants
- **`@n8n/utils`**: Utility functions
- **`@n8n/di`**: Dependency injection
- **`@n8n/decorators`**: TypeScript decorators
- **`@n8n/db`**: Database utilities and schemas

#### Frontend Ecosystem
- **`@n8n/design-system`**: UI component library
- **`@n8n/stores`**: Pinia stores for state management
- **`@n8n/composables`**: Vue composables
- **`@n8n/i18n`**: Internationalization
- **`@n8n/rest-api-client`**: API client

#### Development Tools
- **`@n8n/eslint-config`**: ESLint configuration
- **`@n8n/typescript-config`**: TypeScript configurations
- **`@n8n/vitest-config`**: Testing configuration
- **`@n8n/backend-test-utils`**: Backend testing utilities

#### Advanced Features
- **`@n8n/nodes-langchain`**: LangChain AI integration nodes
- **`@n8n/ai-workflow-builder`**: AI-powered workflow creation
- **`@n8n/task-runner`**: Task execution system
- **`@n8n/permissions`**: Permission management system
- **`@n8n/client-oauth2`**: OAuth2 client implementation

## Windows Installation Dependencies

### Prerequisites for Windows Development

**Required Software**:
1. **Node.js** (>=22.16): Download from [nodejs.org](https://nodejs.org/)
2. **Git**: For version control
3. **Windows Build Tools**: Required for native module compilation
   ```bash
   npm add -g windows-build-tools
   ```

**Package Manager Setup**:
1. **Enable Corepack** (run as Administrator):
   ```bash
   corepack enable
   corepack prepare --activate
   ```
2. **pnpm** will be automatically available via corepack

**Development Environment**:
- **Visual Studio Code** (recommended)
- **Windows Terminal** or **PowerShell** (for better terminal experience)

### Installation Steps for Windows

1. **Clone the repository**:
   ```bash
   git clone https://github.com/n8n-io/n8n.git
   cd n8n
   ```

2. **Install dependencies**:
   ```bash
   pnpm install
   ```

3. **Build the project**:
   ```bash
   pnpm build
   ```

4. **Start development server**:
   ```bash
   pnpm dev
   ```

### Windows-Specific Considerations

- **Administrator privileges** may be required for corepack setup
- **Windows Build Tools** are essential for compiling native dependencies
- **Long path support** should be enabled in Windows for deep node_modules
- **Antivirus exclusions** may be needed for the project directory to improve performance

### Alternative: Dev Container (Recommended for Windows)

For the best Windows development experience, use the provided Dev Container:
1. Install **Docker Desktop** and **VS Code**
2. Install the **Dev Containers** extension
3. Open the project in VS Code and select "Reopen in Container"

This provides a consistent Linux-based development environment without Windows-specific setup issues.

## Development Workflow

### Build System
- **Turborepo**: Orchestrates builds across packages
- **TypeScript**: Compiled with tsc and tsc-alias
- **Vite**: Frontend bundling and development server
- **pnpm**: Package management with workspaces

### Key Scripts
```bash
# Development
pnpm dev                    # Start all development servers
pnpm dev:be                # Backend only
pnpm dev:fe                # Frontend only

# Building
pnpm build                 # Build all packages
pnpm build:backend         # Backend packages only
pnpm build:frontend        # Frontend packages only

# Testing
pnpm test                  # Run all tests
pnpm test:backend          # Backend tests
pnpm test:frontend         # Frontend tests

# Quality
pnpm lint                  # Lint all packages
pnpm format                # Format code
pnpm typecheck             # Type checking
```

### Database Support
- **SQLite**: Default, file-based
- **PostgreSQL**: Production recommended
- **MySQL**: Supported
- **MariaDB**: Supported

## Key Technologies

### Backend Stack
- **Node.js** (>=22.16): Runtime environment
- **TypeScript**: Primary language
- **Express.js**: Web framework
- **TypeORM**: Database ORM
- **Bull**: Job queue system
- **OCLIF**: CLI framework
- **JWT**: Authentication
- **Winston**: Logging

### Frontend Stack
- **Vue.js 3**: UI framework with Composition API
- **TypeScript**: Type safety
- **Vite**: Build tool and dev server
- **Element Plus**: UI component library
- **Vue Flow**: Workflow canvas
- **CodeMirror**: Code editor
- **Pinia**: State management
- **Vue Router**: Routing
- **Vue I18n**: Internationalization

### Development Tools
- **Turborepo**: Monorepo build system
- **pnpm**: Package manager
- **Biome**: Code formatting and linting
- **ESLint**: Additional linting
- **Vitest**: Testing framework
- **Lefthook**: Git hooks
- **Docker**: Containerization

## Testing Infrastructure

### Test Structure
```
cypress/                   # E2E tests
├── e2e/                  # End-to-end test specs
├── fixtures/             # Test data
├── composables/          # Test utilities
└── support/              # Test configuration

test-workflows/           # Workflow test cases
├── workflows/            # Test workflow definitions
├── snapshots/            # Expected outputs
└── testData/             # Test input data
```

### Testing Strategy
- **Unit Tests**: Jest/Vitest for individual components
- **Integration Tests**: API and service testing
- **E2E Tests**: Cypress for full workflow testing
- **Workflow Tests**: Automated workflow execution validation

## Enterprise Features

Located in `.ee` suffixed directories:
- **SSO Integration**: SAML, OAuth2, LDAP
- **Advanced Permissions**: Role-based access control
- **License Management**: Enterprise license validation
- **Audit Logging**: Comprehensive activity tracking
- **Advanced Scaling**: Multi-instance coordination

## Extension System

### Node Development
- **`packages/node-dev/`**: Tools for creating custom nodes
- **Extension SDK**: Framework for building extensions
- **Custom Credentials**: Authentication for custom services

### Plugin Architecture
- Modular node system
- Dynamic loading of community nodes
- Credential type system
- Webhook and trigger support

## Configuration Management

### Environment Variables
- Database configuration
- Authentication settings
- Feature flags
- External service credentials
- Scaling parameters

### Config Files
- **`@n8n/config`**: Centralized configuration management
- Environment-specific overrides
- Runtime configuration validation

## Security Features

- **Credential Encryption**: Secure storage of API keys
- **Expression Sandboxing**: Safe code execution
- **CSRF Protection**: Cross-site request forgery prevention
- **Rate Limiting**: API abuse prevention
- **Input Validation**: Data sanitization
- **Audit Trails**: Security event logging

## Deployment Options

### Self-Hosted
- **Docker**: Official container images
- **npm**: Direct Node.js installation
- **Kubernetes**: Helm charts available
- **Docker Compose**: Multi-service orchestration

### Cloud
- **n8n Cloud**: Managed hosting service
- **Enterprise**: On-premises with support

## Community & Ecosystem

- **400+ Integrations**: Built-in service connections
- **900+ Templates**: Ready-to-use workflows
- **Community Forum**: Support and discussions
- **GitHub**: Open source development
- **Documentation**: Comprehensive guides and API docs

## Recent Updates (v1.100.0)

- Enhanced AI capabilities with LangChain integration
- Improved workflow builder with AI assistance
- Updated dependencies and security patches
- Performance optimizations
- Extended API capabilities
- Enhanced enterprise features

This index provides a comprehensive overview of the n8n codebase structure, architecture, and development ecosystem as of version 1.100.0.
