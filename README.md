# AgentBay CLI

A command-line interface for AgentBay services.

## Features

AgentBay CLI provides comprehensive image management capabilities:

**Note**: The current version of the CLI tool supports creating and activating CodeSpace type images only.

- **Authentication**: Secure OAuth-based login with Google account integration
- **Image Creation**: Build custom images from Dockerfiles with base image support
- **Image Management**: Activate, deactivate, and monitor image instances
- **Image Listing**: Browse user and system images with separated display, pagination and filtering support
- **Configuration Management**: Secure token storage and automatic token refresh

## Installation

### Prerequisites
- Go 1.23.0 or higher
- Make

### Build from Source

```bash
# Clone the repository
git clone https://github.com/agentbay/agentbay-cli.git
cd agentbay-cli

# Install dependencies and build
make install
```

Alternatively, you can build without installing:

```bash
# Build the binary
make build

# Run directly
./agentbay --help
```

### Verify Installation

```bash
agentbay version
```

## Quick Start

```bash
# 1. Log in to AgentBay
agentbay login

# 2. List available images
agentbay image list                    # List user images (default)
agentbay image list --include-system   # List both user and system images
agentbay image list --system-only      # List only system images

# 3. Create a custom image (using system image as base)
agentbay image create myapp --dockerfile ./Dockerfile --imageId code-space-debian-12

# 4. Activate the image
agentbay image activate imgc-xxxxx...xxx

# 5. Deactivate when done
agentbay image deactivate imgc-xxxxx...xxx
```

## Image Management

### Listing Images

```bash
# List user images only (default behavior)
agentbay image list

# Include both user and system images with separated sections
agentbay image list --include-system

# Show only system images (available as base images)
agentbay image list --system-only

# Filter by OS type
agentbay image list --os-type Linux
agentbay image list --include-system --os-type Linux
```

### Creating Custom Images

```bash
# Use system image as base (recommended)
agentbay image create my-custom-env --dockerfile ./Dockerfile --imageId code-space-debian-12

# Use another user image as base
agentbay image create my-variant --dockerfile ./Dockerfile --imageId imgc-xxxxxxxxxxxxx
```

### Managing Image Lifecycle

```bash
# Activate user image (creates compute resources)
agentbay image activate imgc-xxxxxxxxxxxxx

# Activate with specific resources
agentbay image activate imgc-xxxxxxxxxxxxx --cpu 4 --memory 8

# Deactivate when done (releases resources)
agentbay image deactivate imgc-xxxxxxxxxxxxx
```

**Note**: System images are always available and don't require activation. Only user-created images need to be activated before use.

For detailed usage instructions and examples, see the [User Guide](docs/USER_GUIDE.md).


## License

This project is licensed under the Apache License 2.0 - see the LICENSE file for details. 