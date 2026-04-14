# Linux App Builds

Note: This readme was AI generated.

This repository contains GitHub Actions workflows to build various Linux applications in a distribution-agnostic manner, primarily designed for use with [Homebrew Cask](https://github.com/Homebrew/homebrew-cask).

## Purpose

The goal of this repository is to provide reliable, automated builds of Linux applications that can be easily distributed and installed across different Linux distributions. These builds are specifically crafted to work seamlessly with Homebrew Cask's package management system.

## Features

- **Distribution Agnostic**: Builds work across multiple Linux distributions
- **Static Builds**: Where possible, creates static binaries with minimal dependencies
- **Automated Releases**: GitHub Actions automatically build and release packages
- **Homebrew Cask Ready**: Packages are structured for easy integration with Homebrew Cask
- **Multiple Variants**: Different build configurations for various use cases

## Currently Supported Applications

### Emacs with PGTK

- **File**: `.github/workflows/build-emacs-pgtk.yaml`
- **Features**:
  - Pure GTK (PGTK) support for native Wayland and X11 compatibility
  - Native compilation (AOT) for faster Elisp execution
  - Tree-sitter support for modern syntax highlighting
  - Full feature set including JSON, XML2, GnuTLS, SQLite3, Cairo graphics
  - Image format support (JPEG, PNG, GIF, TIFF, WebP, SVG)
- **Build Variants**:
  - **Alpine Linux (musl)**: Static build with minimal dependencies
  - **Fedora Latest**: Dynamic build with latest libraries

### asusctl

- **File**: `.github/workflows/build-asusctl.yaml`
- **Purpose**:
  - Builds the `asusctl` suite as a Cask-friendly `usr/` install root archive
  - Ships the main binaries plus the service, udev, DBus, desktop, icon, aura,
    and anime support files that downstream packaging needs
- **Included Programs**:
  - `asusctl`
  - `asusd`
  - `asus-shutdown`
  - `asusd-user`
  - `rog-control-center`
- **Packaging Notes**:
  - Applies a local patch from `patches/asusctl-xdg-paths.patch`
  - User-space data lookups prefer XDG-style locations such as
    `~/.local/share` and `~/.config`
  - The root daemon units can override binary paths through
    `/etc/asusd/asusd.env`
  - The user daemon unit can override its binary path through
    `~/.config/asusd/asusd-user.env`

## Usage

### For End Users

1. Download the appropriate build from the [Releases](../../releases) page
2. Extract the archive: `tar -xzf <package-name>.tar.gz`
3. Run the application using the included startup script

### For Homebrew Cask Integration

The builds in this repository are designed to be consumed by Homebrew Cask formulas. The release artifacts include:

- Pre-compiled binaries
- Startup scripts with proper environment setup
- Package metadata and build information
- Self-contained directory structure

### For Developers

To add a new application build:

1. Create a new GitHub Actions workflow in `.github/workflows/`
2. Follow the existing patterns for distribution-agnostic builds
3. Ensure the build produces self-contained packages
4. Include proper metadata and startup scripts

## Build Process

Each workflow typically:

1. **Multi-distribution builds** using Docker containers
2. **Dependency installation** for each target distribution
3. **Source code compilation** with optimized flags
4. **Package creation** with startup scripts and metadata
5. **Automated testing** to verify functionality
6. **Release creation** with downloadable artifacts

## Contributing

Contributions are welcome! Please:

1. Follow the existing workflow patterns
2. Test builds thoroughly across distributions
3. Include proper documentation and metadata
4. Ensure compatibility with Homebrew Cask requirements

## License

This repository contains build scripts and workflows. The actual applications built here retain their original licenses. Please refer to each application's source repository for licensing information.

## Support

For issues with:

- **Build workflows**: Open an issue in this repository
- **Application bugs**: Report to the upstream application repository
- **Homebrew Cask integration**: Report to the relevant Cask repository
