# Requirements
- Podman or Docker installed
- Your ZMK config repo with build.yaml and config/west.yml

ZMK Firmware Local Build Script Using Containerized Environment

The script allows you to build ZMK firmware targets defined in a YAML configuration file without the need to install all build dependencies locally. It uses a container runtime (Podman or Docker) to run the build environment.

Usage: ./build_local.sh [flags] <command>

Commands:
```bash 
  init             Initialize the repository (west init + update)
  update           Update the repository (west update)
  list             List all available build targets from build.yaml
  build [name]     Build all firmware or specific target by name
  clean [target]   Clean build directory (all or specific target)
  clean_all        Clean all west dependencies and build artifacts
  gitignore        Generate/update .gitignore from config/west.yml
  copy [dest]      Copy build artifacts to directory (default: ./artifacts)
  help             Show this help message
```

Environment Variables:
```bash
  KEYBOARD        Name of the keyboard being built (default: extracted from directory name)
  RUNTIME         Container runtime (default: podman, can be docker)
  ZMK_IMAGE       ZMK build image (default: docker.io/zmkfirmware/zmk-build-arm:4.1-branch)  
  BUILD_CONFIG    Build configuration file (default: build.yaml)
  INCREMENTAL     Skip pristine builds for faster rebuilds (default: false)
```

Examples:
```bash
  ./build_local.sh list                                                   # List all available targets
  ./build_local.sh build                                                  # Build all firmware from build.yaml
  ./build_local.sh build corne_choc_pro_left_nice_view                    # Build specific target
  ./build_local.sh clean                                                  # Clean build artifacts
  ./build_local.sh clean corne_choc_pro_left_nice_view                    # Clean specific target
  ./build_local.sh clean_all                                              # Clean all west dependencies
  ./build_local.sh gitignore                                              # Update .gitignore from west.yml
  ./build_local.sh copy                                                   # Copy artifacts to ./artifacts
  ./build_local.sh copy /path/to/dir                                      # Copy artifacts to custom directory
  INCREMENTAL=true ./build_local.sh build corne_choc_pro_left_nice_view   # Faster incremental build
  BUILD_CONFIG=custom.yaml ./build_local.sh build                         # Use custom build config
  RUNTIME=docker ./build_local.sh build                                   # Use docker instead of podman
```
