# Weblate MCP Server

A [Model Context Protocol (MCP)](https://modelcontextprotocol.io/) server that provides seamless integration with Weblate translation management platform. This server enables AI assistants to interact directly with your Weblate instance for comprehensive translation management.

## 🌟 Features

- **🔧 Complete Weblate API Access**: Full integration with Weblate's REST API
- **🤖 AI-Powered Workflow**: Natural language interaction with your translation projects
- **📊 Project Management**: Create, list, and manage translation projects
- **🔍 Component Operations**: Handle translation components and configurations
- **✏️ Translation Management**: Update, search, and manage translations
- **🌐 Language Support**: Work with all supported languages in your Weblate instance
- **🚀 Multiple Transports**: HTTP/SSE, Streamable HTTP, and STDIO support
- **🛡️ Type Safety**: Full TypeScript implementation with comprehensive error handling

## 🎯 What is This?

This MCP server acts as a bridge between AI assistants (like Claude Desktop) and your Weblate translation management platform. Instead of manually navigating the Weblate web interface, you can use natural language to:

- **"List all projects in my Weblate instance"**
- **"Show me the French translations for the frontend component"**
- **"Update the welcome message translation"**
- **"Create a new translation project"**

## 🚀 Quick Start

### Option 1: Use with npx (Recommended)

The easiest way to use this MCP server is with npx - no installation required!

**For Claude Desktop or other MCP clients:**
```json
{
  "mcpServers": {
    "weblate": {
      "command": "npx",
      "args": ["-y", "@mmntm/weblate-mcp"],
      "env": {
        "WEBLATE_API_URL": "https://your-weblate-instance.com/api",
        "WEBLATE_API_TOKEN": "your-weblate-api-token"
      }
    }
  }
}
```

**Manual testing:**
```bash
# Test the server directly
npx @mmntm/weblate-mcp
```

### Option 2: Development Setup

### Prerequisites
- Node.js 18+
- pnpm package manager
- Weblate instance with API access

### Installation
```bash
# Clone and install
git clone <this-repo>
cd weblate-mcp
pnpm install

# Configure environment
cp .env.example .env
# Edit .env with your Weblate API URL and token

# Build and start
pnpm build
pnpm start
```

Server runs on `http://localhost:3001` by default.

### Environment Configuration
```env
WEBLATE_API_URL=https://your-weblate-instance.com
WEBLATE_API_TOKEN=your-api-token-here
PORT=3001
NODE_ENV=production
LOG_LEVEL=info
```

## 🔗 MCP Client Configuration

### Claude Desktop (npx method - Recommended)
Add to your Claude Desktop config (`~/Library/Application Support/Claude/claude_desktop_config.json`):
```json
{
  "mcpServers": {
    "weblate": {
      "command": "npx",
      "args": ["-y", "@mmntm/weblate-mcp"],
      "env": {
        "WEBLATE_API_URL": "https://your-weblate-instance.com/api",
        "WEBLATE_API_TOKEN": "your-weblate-api-token"
      }
    }
  }
}
```

### Claude Desktop (Development/Local)
For development or local builds:
```json
{
  "mcpServers": {
    "weblate": {
      "command": "node",
      "args": ["/path/to/weblate-mcp/dist/main.js"],
      "env": {
        "WEBLATE_API_URL": "https://your-weblate-instance.com/api",
        "WEBLATE_API_TOKEN": "your-api-token"
      }
    }
  }
}
```

### HTTP Clients (Cursor, VS Code, Web Apps)
```json
{
  "transport": "http",
  "url": "http://localhost:3001/mcp"
}
```

## 🛠️ Available Tools

### 📊 Project Management
| Tool | Description |
|------|-------------|
| **`listProjects`** | List all available Weblate projects with URLs and metadata |

### 🔧 Component Management
| Tool | Description |
|------|-------------|
| **`listComponents`** | List components in a specific project with source language details |

### ✏️ Translation Management
| Tool | Description |
|------|-------------|
| **`searchStringInProject`** | Search for translations containing specific text in a project |
| **`getTranslationForKey`** | Get translation value for a specific key |
| **`writeTranslation`** | Update or write translation values with approval support |
| **`searchTranslationsByKey`** | Search for translations by key pattern across components |
| **`findTranslationsForKey`** | Find all translations for a specific key across languages |
| **`listTranslationKeys`** | List all translation keys in a project (filterable by component) |
| **`searchTranslationKeys`** | Search for translation keys by pattern in a project |

### 🌐 Language Management
| Tool | Description |
|------|-------------|
| **`listLanguages`** | List languages available in a specific project |

### 📊 Translation Statistics Dashboard
| Tool | Description |
|------|-------------|
| **`getProjectStatistics`** | Comprehensive project statistics with completion rates and string counts |
| **`getComponentStatistics`** | Detailed statistics for a specific component |
| **`getProjectDashboard`** | Complete dashboard overview with all component statistics |
| **`getTranslationStatistics`** | Statistics for specific translation (project/component/language) |
| **`getComponentLanguageProgress`** | Translation progress for all languages in a component with progress bars |
| **`getLanguageStatistics`** | Statistics for a language across all projects |
| **`getUserStatistics`** | User contribution statistics and activity metrics |

### 📈 Change Tracking & History
| Tool | Description |
|------|-------------|
| **`listRecentChanges`** | Recent changes across all projects with user and timestamp filtering |
| **`getProjectChanges`** | Recent changes for a specific project |
| **`getComponentChanges`** | Recent changes for a specific component |
| **`getChangesByUser`** | Recent changes by a specific user |

## 💡 Usage Examples

### Project Operations
```typescript
// List all projects
await list_projects();

// Get specific project details
await get_project({ slug: "my-project" });

// Create a new project
await create_project({
  name: "New Project",
  slug: "new-project",
  web: "https://example.com"
});
```

### Translation Operations
```typescript
// List translations for a component
await list_translations({
  project_slug: "my-project",
  component_slug: "frontend"
});

// Get specific translation
await get_translation({
  project_slug: "my-project",
  component_slug: "frontend",
  language_code: "fr"
});

// Update translations
await update_translation({
  project_slug: "my-project",
  component_slug: "frontend",
  language_code: "fr",
  translations: {
    "welcome": "Bienvenue",
    "goodbye": "Au revoir"
  }
});
```

## 📚 Documentation

| Document | Description |
|----------|-------------|
| **[📖 Documentation Hub](./docs/README.md)** | Complete documentation overview and quick start |
| **[🚀 Installation & Setup](./docs/MCP_SETUP.md)** | Installation, configuration, and Claude Desktop setup |
| **[📋 API Reference](./docs/API.md)** | Complete API documentation with examples |
| **[🛠️ Development Guide](./docs/DEVELOPMENT.md)** | Contributing, development setup, and testing |
| **[🏗️ Architecture](./docs/ARCHITECTURE.md)** | Codebase structure, patterns, and design decisions |
| **[📦 Release Process](./docs/RELEASE.md)** | Release management and publishing workflow |
| **[🔄 Changesets Guide](./docs/CHANGESETS.md)** | Version management with changesets |

## 🏗️ Architecture

```
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│   MCP Client    │───▶│  Weblate MCP     │───▶│  Weblate API    │
│  (IDE/Editor)   │    │     Server       │    │   (REST API)    │
└─────────────────┘    └──────────────────┘    └─────────────────┘
                              │
                              ▼
                       ┌──────────────────┐
                       │   MCP Tools      │
                       │ • Projects       │
                       │ • Components     │
                       │ • Translations   │
                       │ • Languages      │
                       └──────────────────┘
```

**Technology Stack:**
- **NestJS**: Modern Node.js framework with dependency injection
- **TypeScript**: Full type safety and IntelliSense support
- **Weblate REST API**: Comprehensive API wrapper with interfaces
- **MCP Protocol**: Standard Model Context Protocol implementation
- **Axios**: HTTP client for API communication

## 🧪 Development

### Development Setup
```bash
# Start development server with hot reload
pnpm run dev

# Run tests
pnpm test

# Run end-to-end tests
pnpm run test:e2e

# Generate test coverage
pnpm run test:cov

# Build for production
pnpm build
```

### Adding New Tools
1. Create tool file in `src/tools/`
2. Implement MCP tool interface
3. Add to service providers
4. Write tests
5. Update documentation

See [Development Guide](./docs/DEVELOPMENT.md) for detailed instructions.

## 🎯 Use Cases

### Translation Management
- **Project oversight**: Monitor translation progress across projects
- **Content updates**: Update translations programmatically
- **Quality assurance**: Review and approve translations
- **Team coordination**: Manage translation workflows

### Development Integration
- **CI/CD pipelines**: Automate translation updates in deployment
- **Content management**: Sync translations with content systems
- **Localization testing**: Validate translations in different contexts
- **Documentation**: Generate translation reports and statistics

### AI-Assisted Workflows
- **Natural language queries**: Ask about translation status in plain English
- **Contextual operations**: AI understands your translation needs
- **Batch operations**: Perform bulk updates with AI assistance
- **Smart suggestions**: Get AI-powered translation recommendations

## 🔒 Security & Production

- **API Token Security**: Store tokens securely, use environment variables
- **Rate Limiting**: Built-in request throttling and retry logic
- **Error Handling**: Comprehensive error responses with debugging info
- **Input Validation**: All inputs validated with Zod schemas
- **HTTPS Support**: Secure communication with Weblate instances

## 🤝 Contributing

We welcome contributions! Please see our [Contributing Guidelines](./docs/DEVELOPMENT.md#contributing):

1. **Fork** the repository
2. **Create** a feature branch from main
3. **Implement** changes with tests
4. **Update** documentation
5. **Submit** a pull request

### Code Style
- Use TypeScript for type safety
- Follow NestJS conventions
- Add comprehensive tests
- Update documentation

## 📄 License

MIT License - see [LICENSE](./LICENSE) file for details.

## 🙏 Acknowledgments

- **Weblate**: For providing an excellent translation management platform
- **Model Context Protocol**: For the standardized protocol specification
- **NestJS**: For the robust application framework
- **Contributors**: Everyone who helps improve this project

---

**Built with ❤️ for the translation community**

*Need help? Check our [documentation](./docs/) or create an [issue](https://github.com/mmntm/weblate-mcp/issues)!* 