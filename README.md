# CasaOS for PowerPC G5

This directory contains CasaOS packages specifically designed for Apple Power Mac G5 and other PowerPC 64-bit systems.

## Package Contents

- **Source Code**: Full CasaOS v0.4.15 source code (in casaos-source/)
- **Init Scripts**: runit service definitions  
- **Web UI**: Complete CasaOS web interface (39MB)
- **Build Instructions**: Step-by-step compilation guide
- **Licensing**: Apache 2.0 with proper attribution

## Why No Binaries?

Cross-compilation from x86 to PowerPC fails due to platform-specific dependencies (`modernc.org/libc` used by SQLite). You must build directly on your PowerPC system.

## Installation Options

### Option 1: Debian Package (.deb)
```bash
# On your PowerPC G5:
sudo dpkg -i packages/ppc64-casaos-runit_0.4.15_ppc64.deb
```

### Option 2: Tarball (.tar.gz)
```bash
# On your PowerPC G5:
sudo tar -xzf packages/ppc64-casaos-runit_0.4.15.tar.gz -C /
```

## After Installation

1. **Read the build guide**:
   ```bash
   cat /usr/share/doc/casaos/BUILD-ON-PPC64.md
   ```

2. **Compile binaries on your G5**:
   - Install Go for PowerPC
   - Build all 6 microservices  
   - Copy binaries to `/usr/bin/`

3. **Install Podman** (Docker not available on PowerPC):
   ```bash
   sudo apt install podman
   ```

4. **Start services**:
   ```bash
   sudo sv start casaos-message-bus
   sudo sv start casaos-gateway
   sudo sv start casaos-user-service
   sudo sv start casaos-local-storage
   sudo sv start casaos-app-management
   sudo sv start casaos
   ```

5. **Access CasaOS**:
   Open browser to `http://your-g5-ip/`

## PowerPC-Specific Notes

### Podman vs Docker
- Docker is **NOT available** for PowerPC
- This package uses Podman (Docker-compatible)
- Automatic docker→podman symlink created during installation

### Container Availability
⚠️ **Limited Container Ecosystem**
- Most Docker Hub images are amd64/arm64 only
- Very few ppc64 container images exist
- You may need to build custom containers from source

### Supported Distributions
- Void Linux PowerPC (runit)
- Gentoo Linux PowerPC
- Debian PowerPC  
- Other ppc64 Linux distributions with runit

## File Structure

```
casaos-ppc64/
├── README.md (this file)
├── BUILD-ON-PPC64.md (detailed build instructions)
├── casaos-source/ (full source code for all services)
│   ├── CasaOS/
│   ├── CasaOS-MessageBus/
│   ├── CasaOS-Gateway/
│   ├── CasaOS-UserService/
│   ├── CasaOS-LocalStorage/
│   └── CasaOS-AppManagement/
└── packages/
    ├── ppc64-casaos-runit_0.4.15_ppc64.deb (71MB)
    └── ppc64-casaos-runit_0.4.15.tar.gz (81MB)
```

## Version Information

- CasaOS: v0.4.15
- CasaOS-UI: v0.4.15
- Microservices:
  - message-bus: v0.4.4
  - gateway: v0.4.8
  - user-service: v0.4.8
  - local-storage: v0.4.4
  - app-management: v0.4.5

## Legal & Licensing

This PowerPC port is licensed under Apache License 2.0, same as the original CasaOS project.

**Community Contribution Disclaimer:**
> "i wouldnt use this on production builds unless you tested it to deth if i was you heh"

This is a personal one-off port for enthusiasts with PowerPC hardware. Use at your own risk.

## Support

- Original CasaOS: https://github.com/IceWhaleTech/CasaOS
- Build Issues: Compile on actual PowerPC hardware
- Container Issues: Limited ppc64 image availability

---

**Keep that beautiful G5 tower useful! 🍎⚡**
