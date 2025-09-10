# .NET Dev Container Template

A ready-to-use development container template for .NET projects, providing a consistent and reproducible development environment using Visual Studio Code Dev Containers.

## 🎯 What is this?

This repository serves as a template for creating .NET development environments using [Visual Studio Code Dev Containers](https://code.visualstudio.com/docs/devcontainers/containers). It provides a pre-configured development container that includes:

- **.NET SDK 9.0** running on Alpine Linux
- **C# extension** for Visual Studio Code
- **Optimized container setup** for .NET development

## ✅ Prerequisites

Before using this template, ensure you have:

- [Docker](https://docs.docker.com/get-docker/) installed and running
- [Visual Studio Code](https://code.visualstudio.com/) installed
- [Dev Containers extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) for VS Code

## 🚀 Getting Started

### Option 1: Use as Template (Recommended)

1. **Create a new repository** from this template:
   - Click the "Use this template" button on GitHub
   - Name your new repository
   - Clone your new repository locally

2. **Open in Dev Container**:
   ```bash
   git clone https://github.com/yourusername/your-new-repo.git
   cd your-new-repo
   code .
   ```

3. **Reopen in Container**:
   - VS Code will prompt you to "Reopen in Container"
   - Or use Command Palette (`Ctrl+Shift+P` / `Cmd+Shift+P`) → "Dev Containers: Reopen in Container"

### Option 2: Clone and Modify

```bash
git clone https://github.com/preston176/dotnet-devcontainer-template.git
cd dotnet-devcontainer-template
code .
```

### Option 3: Add to Existing Project

Copy the `.devcontainer` folder to your existing .NET project root directory.

## 📦 What's Included

### Container Configuration

- **Base Image**: `mcr.microsoft.com/dotnet/sdk:9.0-alpine`
  - Lightweight Alpine Linux distribution
  - Complete .NET 9.0 SDK
  - Ready for both development and building

### VS Code Extensions

- **C# for Visual Studio Code** (`ms-dotnettools.csharp`)
  - Syntax highlighting
  - IntelliSense
  - Debugging support
  - Code navigation

### Development Tools

The container includes all standard .NET CLI tools:
- `dotnet new` - Create new projects
- `dotnet build` - Build projects
- `dotnet run` - Run applications
- `dotnet test` - Run unit tests
- `dotnet publish` - Publish applications

## 🛠️ Creating Your First .NET Project

Once your dev container is running:

### Console Application
```bash
dotnet new console -n MyConsoleApp
cd MyConsoleApp
dotnet run
```

### Web API
```bash
dotnet new webapi -n MyWebApi
cd MyWebApi
dotnet run
```

### Class Library
```bash
dotnet new classlib -n MyLibrary
```

### Solution with Multiple Projects
```bash
dotnet new sln -n MySolution
dotnet new console -n MyApp
dotnet new classlib -n MyLibrary
dotnet sln add MyApp MyLibrary
dotnet add MyApp reference MyLibrary
```

## ⚙️ Customization

### Adding VS Code Extensions

Edit `.devcontainer/devcontainer.json` to add more extensions:

```json
{
  "image": "mcr.microsoft.com/dotnet/sdk:9.0-alpine",
  "customizations": {
    "vscode": {
      "extensions": [
        "ms-dotnettools.csharp",
        "ms-dotnettools.vscode-dotnet-runtime",
        "formulahendry.dotnet-test-explorer",
        "jchannon.csharpextensions"
      ]
    }
  }
}
```

### Popular .NET Extensions

- `ms-dotnettools.vscode-dotnet-runtime` - .NET Runtime extension
- `formulahendry.dotnet-test-explorer` - Test explorer
- `jchannon.csharpextensions` - C# productivity extensions
- `ms-vscode.vscode-json` - JSON support
- `redhat.vscode-yaml` - YAML support

### Changing .NET Version

To use a different .NET version, update the image in `devcontainer.json`:

```json
{
  "image": "mcr.microsoft.com/dotnet/sdk:8.0-alpine"  // For .NET 8
}
```

Available versions:
- `mcr.microsoft.com/dotnet/sdk:9.0-alpine` (.NET 9)
- `mcr.microsoft.com/dotnet/sdk:8.0-alpine` (.NET 8)
- `mcr.microsoft.com/dotnet/sdk:6.0-alpine` (.NET 6 LTS)

### Adding Development Dependencies

Create a `Dockerfile` for custom dependencies:

1. Create `.devcontainer/Dockerfile`:
```dockerfile
FROM mcr.microsoft.com/dotnet/sdk:9.0-alpine

# Install additional tools
RUN apk add --no-cache git curl wget

# Install global .NET tools
RUN dotnet tool install -g dotnet-ef
```

2. Update `devcontainer.json`:
```json
{
  "build": {
    "dockerfile": "Dockerfile"
  },
  "customizations": {
    "vscode": {
      "extensions": ["ms-dotnettools.csharp"]
    }
  }
}
```

### Environment Variables

Add environment variables to your dev container:

```json
{
  "image": "mcr.microsoft.com/dotnet/sdk:9.0-alpine",
  "containerEnv": {
    "ASPNETCORE_ENVIRONMENT": "Development",
    "DOTNET_WATCH_RESTART_ON_RUDE_EDIT": "true"
  }
}
```

### Port Forwarding

Forward ports for web applications:

```json
{
  "image": "mcr.microsoft.com/dotnet/sdk:9.0-alpine",
  "forwardPorts": [5000, 5001, 7000, 7001],
  "portsAttributes": {
    "5000": {
      "label": "HTTP",
      "protocol": "http"
    },
    "5001": {
      "label": "HTTPS",
      "protocol": "https"
    }
  }
}
```

## 🎯 Common Use Cases

### Web Development
Perfect for ASP.NET Core applications, Web APIs, and Blazor projects.

### Microservices
Ideal for developing containerized microservices with consistent environments.

### Library Development
Great for creating and testing .NET class libraries and NuGet packages.

### Learning and Tutorials
Excellent for .NET learning environments and coding tutorials.

### Team Collaboration
Ensures all team members work in identical development environments.

## 🔧 Troubleshooting

### Container Won't Start

1. **Check Docker is running**:
   ```bash
   docker --version
   docker ps
   ```

2. **Restart Docker Desktop** if needed

3. **Clear Docker cache**:
   ```bash
   docker system prune -a
   ```

### Extensions Not Loading

1. **Rebuild container**: Command Palette → "Dev Containers: Rebuild Container"
2. **Check extension IDs** in `devcontainer.json`
3. **Clear VS Code workspace settings**

### Slow Performance

1. **Enable file watching exclusions** in `.gitignore`
2. **Use volume mounts** for better performance
3. **Consider using WSL2** on Windows

### Port Already in Use

```bash
# Find process using the port
sudo lsof -i :5000
# Kill the process
kill -9 <PID>
```

## 🤝 Contributing

We welcome contributions! Please:

1. **Fork the repository**
2. **Create a feature branch**: `git checkout -b feature/amazing-feature`
3. **Commit changes**: `git commit -m 'Add amazing feature'`
4. **Push to branch**: `git push origin feature/amazing-feature`
5. **Open a Pull Request**

### Contribution Ideas

- Additional VS Code extensions
- Support for different .NET versions
- Documentation improvements
- Example projects
- Performance optimizations

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- [Microsoft .NET Team](https://github.com/dotnet) for the excellent .NET SDK
- [VS Code Dev Containers team](https://github.com/microsoft/vscode-dev-containers) for the amazing dev containers technology
- [Docker](https://www.docker.com/) for containerization platform

## 📚 Additional Resources

- [.NET Documentation](https://docs.microsoft.com/en-us/dotnet/)
- [VS Code Dev Containers Documentation](https://code.visualstudio.com/docs/devcontainers/containers)
- [Docker Documentation](https://docs.docker.com/)
- [Alpine Linux](https://alpinelinux.org/)

---

**Happy coding! 🚀**

*For questions or support, please open an issue in this repository.*