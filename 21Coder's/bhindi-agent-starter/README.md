# Bhindi Agent Starter Kit

A TypeScript-based agent starter kit that demonstrates both **public calculator tools** and **authenticated GitHub tools**. Perfect for learning agent development with the [Bhindi.io](https://bhindi.io) specification.

# What is Bhindi?
Bhindi lets you talk to your apps like you talk to a friend.
Bhindi supports 100+ integrations and is the easiest way to build AI agents.

Check a list of integrations available at [Bhindi Agents Directory](https://directory.bhindi.io/)

## 📚 Documentation

For comprehensive documentation on building agents, visit the [Bhindi Documentation](https://github.com/upsurgeio/bhindi-docs).

## 🎯 What This Starter Kit Demonstrates

This starter kit teaches you how to build agents with:
- **Public tools** (Calculator - no authentication required)
- **Authenticated tools** (GitHub - Bearer token required)
- **Mixed authentication patterns** in a single agent
- **Proper parameter validation** using JSON Schema
- **Advanced features** like `confirmationRequired`
- **Standardized response formats** following agent specification

## ✨ Features

### Calculator Tools (No Authentication)
- **8 mathematical operations**: Basic arithmetic, power, square root, percentage, factorial
- **Parameter validation**: Proper error handling for invalid inputs
- **Confirmation required**: Demonstrates user confirmation for certain operations

### GitHub Tools (Authentication Required)
- **Repository listing**: List user's GitHub repositories with Bearer token
- **Simple REST API**: Uses standard fetch calls (no heavy dependencies)
- **Authentication demonstration**: Shows how to handle Bearer tokens

### Development Features
- **Full TypeScript support** with strict typing
- **Comprehensive testing** with Jest
- **ESLint + Prettier** for code quality
- **JSON Schema validation** for parameters
- **Standardized error handling**

## 🚀 Available Tools

### Calculator Tools

| Tool | Description | Special Features |
|------|-------------|------------------|
| `add` | Add two numbers | Basic operation |
| `subtract` | Subtract two numbers | `confirmationRequired: true` |
| `multiply` | Multiply two numbers | Basic operation |
| `divide` | Divide two numbers | Error handling for division by zero |
| `power` | Calculate a^b | Supports negative exponents |
| `sqrt` | Square root | Error handling for negative inputs |
| `percentage` | Calculate percentage | Handles decimal percentages |
| `factorial` | Calculate factorial | `confirmationRequired: true` |
| `countCharacter` | Count character occurrences in text | String manipulation |

### GitHub Tools (Private - Auth Required)

| Tool | Description | Authentication |
|------|-------------|----------------|
| `listUserRepositories` | List user's repositories | Bearer token required |

## 📋 Quick Start

### 1. Install Dependencies
```bash
npm install
```

### 2. Build the Project
```bash
npm run build
```

### 3. Start the Server
```bash
npm start
# or for development with auto-reload:
npm run dev
```

### 4. Test the API
```bash
# Get available tools
curl -X GET "http://localhost:3000/tools"

# Test calculator (no auth needed)
curl -X POST "http://localhost:3000/tools/add" \
  -H "Content-Type: application/json" \
  -d '{"a": 5, "b": 3}'

# Test character counting
curl -X POST "http://localhost:3000/tools/countCharacter" \
  -H "Content-Type: application/json" \
  -d '{"character": "s", "text": "strawberrry"}'
```

## 🧮 Usage Examples

### Calculator Tools (No Authentication)

```bash
# Basic addition
curl -X POST "http://localhost:3000/tools/add" \
  -H "Content-Type: application/json" \
  -d '{"a": 10, "b": 5}'

# Division with error handling
curl -X POST "http://localhost:3000/tools/divide" \
  -H "Content-Type: application/json" \
  -d '{"a": 10, "b": 0}'  # Will return error

# Factorial (requires confirmation)
curl -X POST "http://localhost:3000/tools/factorial" \
  -H "Content-Type: application/json" \
  -d '{"number": 5}'

# Percentage calculation
curl -X POST "http://localhost:3000/tools/percentage" \
  -H "Content-Type: application/json" \
  -d '{"percentage": 25, "of": 80}'

# Character counting in text
curl -X POST "http://localhost:3000/tools/countCharacter" \
  -H "Content-Type: application/json" \
  -d '{"character": "s", "text": "strawberrry"}'

# Expected response:
# {
#   "success": true,
#   "responseType": "mixed",
#   "data": {
#     "operation": "Count 's' in \"strawberrry\"",
#     "result": 1,
#     "message": "Calculated Count 's' in \"strawberrry\" = 1",
#     "tool_type": "calculator"
#   }
# }
```

### GitHub Tools (Authentication Required)

```bash
# List repositories (requires GitHub token)
curl -X POST "http://localhost:3000/tools/listUserRepositories" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_GITHUB_TOKEN" \
  -d '{"per_page": 5, "sort": "updated"}'
```

## 🔐 Authentication

This agent demonstrates **hybrid authentication**:

- **Calculator tools**: No authentication required (public)
- **GitHub tools**: Bearer token authentication required (private)

To learn more about authentication, check out the [Bhindi.io Agent Documentation](https://github.com/upsurgeio/bhindi-docs#-authentication)

## 📚 API Endpoints

- `GET /tools` - Get list of available tools (public)
- `POST /tools/:toolName` - Execute a specific tool (auth depends on tool type)
- `GET /health` - Health check endpoint (shows tool authentication requirements)
- `GET /docs` - Swagger UI documentation (serves `public/swagger.json`)

## 📖 Documentation & Examples

- **[Complete API Examples](examples.md)** - Detailed usage examples for all tools with curl commands
- **Swagger Documentation** - Available at `/docs` endpoint when server is running
- **Postman Collection** - Import `Bhind-Agent-Starter.postman_collection.json` for easy testing

## 🏗️ Project Structure

```
src/
├── config/
│   └── tools.json          # Tool definitions with JSON Schema
├── controllers/
│   └── appController.ts    # Handles both calculator & GitHub tools
├── services/
│   ├── calculatorService.ts # Mathematical operations
│   └── githubService.ts     # Simple GitHub API calls
├── routes/
│   ├── toolsRoutes.ts      # GET /tools endpoint
│   └── appRoutes.ts        # POST /tools/:toolName endpoint
├── middlewares/
│   ├── auth.ts             # Authentication utilities
│   └── errorHandler.ts     # Error handling middleware
├── types/
│   └── agent.ts            # Response type definitions
├── __tests__/
│   └── calculatorService.test.ts # Comprehensive tests
├── app.ts                  # Express app configuration
└── server.ts              # Server entry point
```

## 🧪 Development

```bash
# Run tests
npm test

# Run tests in watch mode
npm run test:watch

# Lint code
npm run lint

# Format code
npm run format

# Development server with auto-reload
npm run dev
```

## 🎓 Learning Objectives

This starter kit teaches you:

1. **Agent Architecture**: How to structure tools and services
2. **Mixed Authentication**: Public vs authenticated endpoints
3. **Parameter Validation**: JSON Schema validation patterns
4. **Error Handling**: Proper error responses and status codes
5. **Response Formats**: Standardized success/error responses
6. **Testing**: Comprehensive test coverage patterns
7. **Tool Features**: `confirmationRequired`, parameter types

## 🔧 Advanced Features Demonstrated

- **confirmationRequired**: `subtract` and `factorial` tools
- **Parameter validation**: Type checking and required parameters
- **Enum parameters**: GitHub tool sort/direction options
- **Default values**: Optional parameters with defaults
- **Error handling**: Division by zero, negative square roots, etc.
- **Mixed response types**: Different data structures for different tools

## 🚀 Next Steps

Once you understand this agent, you can:

1. **Add more calculator functions**: Trigonometry, logarithms, etc.
2. **Add more authenticated tools**: Twitter, Slack, database operations
3. **Implement middleware authentication**: Global auth patterns
4. **Add validation middleware**: Request/response validation
5. **Add rate limiting**: Protect expensive operations
6. **Add database integration**: Store calculation history

## 📖 Agent Specification Compliance

This starter follows the [Bhindi.io](https://bhindi.io) agent specification:
- ✅ Required endpoints: `GET /tools`, `POST /tools/:toolName`
- ✅ Standardized response formats: `BaseSuccessResponseDto`, `BaseErrorResponseDto`
- ✅ JSON Schema parameter validation
- ✅ Tool confirmation
- ✅ Authentication patterns (Bearer tokens)
- ✅ Proper error handling and status codes

Perfect for learning how to build production-ready agents! 🎉

## Need Help?

We're here for you! You can reach out to us at:

- **Email**: [info@bhindi.io](mailto:info@bhindi.io)
- **Twitter/X**: [@bhindiai](https://x.com/bhindiai) for the latest updates
- **Discord**: [Join our community](https://discord.gg/hSfTG33ymy)
- **Documentation**: [Bhindi Docs](https://github.com/upsurgeio/bhindi-docs)
- **Website**: [Bhindi.io](https://bhindi.io)
