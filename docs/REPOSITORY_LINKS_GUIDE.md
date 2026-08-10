# Where to Put Repository Links for Your Custom Kernel Build

This guide explains where to properly reference and link to external repositories (OnePlus kernel, NoMount, ReSukiSU) in your kernel build project.

---

## 📍 Primary Repository Structure

Your main repository should have this structure:

```
SSS1981-op/OnePlus_ReSukiSU_SUSFS/
├── README.md                          # ← Main entry point with all links
├── NOMOUNT_BUILD_GUIDE.md            # ← Detailed guide with repo links
├── .github/
│   ├── workflows/
│   │   └── build-nomount-kernel.yml  # ← GitHub Actions with repo URLs
│   └── ISSUE_TEMPLATE/
│       └── bug_report.md             # ← Issues with repo references
├── scripts/
│   ├── build_kernel.sh               # ← Build script with repo cloning
│   └── fetch_sources.sh              # ← Repository fetching script
├── docs/
│   ├── SETUP.md                      # ← Initial setup with all links
│   ├── TROUBLESHOOTING.md            # ← Links to upstream issues
│   └── CONTRIBUTORS.md               # ← Credit upstream projects
├── patches/
│   └── custom/                       # ← Your custom patches
├── config/
│   └── defconfig                     # ← Device configuration
└── kernel/                           # ← Symbolic link or submodule
```

---

## 1️⃣ README.md (Main Entry Point)

**Location:** Repository root  
**Purpose:** First thing users see

```markdown
# OnePlus 13R Custom Kernel with ReSukiSU & NoMount

This project builds a custom kernel for OnePlus 13R with advanced features.

## 📚 Documentation

- [Complete Build Guide](./NOMOUNT_BUILD_GUIDE.md)
- [Setup Instructions](./docs/SETUP.md)
- [Troubleshooting](./docs/TROUBLESHOOTING.md)

## 🔗 Upstream Repositories

| Component | Repository | Purpose |
|-----------|-----------|---------|
| **OnePlus Kernel** | [OnePlusOSS/android_kernel_oneplus_sm8550](https://github.com/OnePlusOSS/android_kernel_oneplus_sm8550) | Base kernel source |
| **ReSukiSU** | [ReSukiSU/ReSukiSU](https://github.com/ReSukiSU/ReSukiSU) | KernelSU with SUSFS |
| **NoMount** | [maxsteeel/nomount](https://github.com/maxsteeel/nomount) | VFS file injection |
| **KernelSU** | [tiann/KernelSU](https://github.com/tiann/KernelSU) | Base root solution |

## 🚀 Quick Start

```bash
# Clone this repository
git clone https://github.com/SSS1981-op/OnePlus_ReSukiSU_SUSFS.git
cd OnePlus_ReSukiSU_SUSFS

# Run the build script (automatically fetches upstream repos)
./scripts/build_kernel.sh
```

## 📖 How to Use

1. See [NOMOUNT_BUILD_GUIDE.md](./NOMOUNT_BUILD_GUIDE.md) for detailed instructions
2. Follow [docs/SETUP.md](./docs/SETUP.md) for initial setup
3. Run `./scripts/build_kernel.sh` to build

## 🙏 Credits

This project is built on top of:
- OnePlus official kernel sources
- ReSukiSU (fork of KernelSU)
- NoMount by @maxsteeel
- KernelSU by @tiann

See [CONTRIBUTORS.md](./docs/CONTRIBUTORS.md) for full credits.
```

---

## 2️⃣ NOMOUNT_BUILD_GUIDE.md

**Location:** Repository root  
**Purpose:** Comprehensive guide with all external links

### Header Section
```markdown
# Complete Guide: Building OnePlus 13R Custom Kernel with ReSukiSU + NoMount

**Base Repository:** https://github.com/OnePlusOSS/android_kernel_oneplus_sm8550  
**ReSukiSU:** https://github.com/ReSukiSU/ReSukiSU  
**NoMount:** https://github.com/maxsteeel/nomount  
**This Project:** https://github.com/SSS1981-op/OnePlus_ReSukiSU_SUSFS  

---

## Quick Links
- [OnePlus OSS Portal](https://opensource.oneplus.com/)
- [KernelSU Documentation](https://kernelsu.org)
- [NoMount GitHub](https://github.com/maxsteeel/nomount)
- [ReSukiSU GitHub](https://github.com/ReSukiSU/ReSukiSU)
```

### In Part 1: Fetching the Kernel
```markdown
### Official Methods

#### Method A: OnePlus OSS GitHub (Recommended)
```bash
git clone https://github.com/OnePlusOSS/android_kernel_oneplus_sm8550.git kernel_op13r
cd kernel_op13r
git checkout OOS15
```

**Repository Details:**
- Owner: [OnePlusOSS](https://github.com/OnePlusOSS)
- Full URL: https://github.com/OnePlusOSS/android_kernel_oneplus_sm8550
- For OnePlus 12 (fallback): https://github.com/OnePlusOSS/android_kernel_oneplus_sm8650

#### Method B: OnePlus Official Portal
Visit: https://opensource.oneplus.com/
```

### In Part 2: Integrating NoMount Patches
```markdown
### Step 1: Clone NoMount Repository

Repository: https://github.com/maxsteeel/nomount

```bash
git clone --branch dev https://github.com/maxsteeel/nomount.git nomount_patch
cd nomount_patch
git log --oneline | head -5
```

**Key Files:**
- Patches: https://github.com/maxsteeel/nomount/tree/master/kernel/patches
- Integration Guide: https://github.com/maxsteeel/nomount/blob/master/kernel/README.md
- Architecture: https://github.com/maxsteeel/nomount/blob/master/kernel/INTEGRATION.md
```

### In References Section
```markdown
## References & Resources

### Official Sources
- **OnePlus Open Source**: https://opensource.oneplus.com/
- **OnePlus GitHub**: https://github.com/OnePlusOSS

### Custom Kernel Projects
- **ReSukiSU**: https://github.com/ReSukiSU/ReSukiSU
- **NoMount Project**: https://github.com/maxsteeel/nomount
- **KernelSU**: https://github.com/tiann/KernelSU

### Documentation
- **KernelSU Docs**: https://kernelsu.org
- **ReSukiSU Guide**: https://ReSukiSU.github.io
- **NoMount Architecture**: https://github.com/maxsteeel/nomount/blob/master/kernel/INTEGRATION.md

### Community Resources
- **XDA Forums**: https://forum.xda-developers.com/
- **OnePlus Community**: https://forums.oneplus.com/

### Related Projects
- **WildKernels**: https://github.com/WildKernels/OnePlus_KernelSU_SUSFS
- **Sukisu Project**: https://github.com/tiann/KernelSU
```

---

## 3️⃣ .github/workflows/build-nomount-kernel.yml

**Location:** `.github/workflows/build-nomount-kernel.yml`  
**Purpose:** CI/CD pipeline with repository URLs

```yaml
name: Build Custom Kernel with NoMount

on:
  push:
    branches:
      - main
      - dev

jobs:
  fetch-kernel:
    name: Fetch OnePlus Kernel
    runs-on: ubuntu-latest
    
    steps:
      - name: Checkout Repository
        uses: actions/checkout@v4
        with:
          repository: SSS1981-op/OnePlus_ReSukiSU_SUSFS
      
      - name: Fetch OnePlus Kernel Source
        run: |
          echo "📥 Cloning OnePlus kernel..."
          # Repository: https://github.com/OnePlusOSS/android_kernel_oneplus_sm8550
          git clone https://github.com/OnePlusOSS/android_kernel_oneplus_sm8550.git kernel_source
          cd kernel_source
          git checkout OOS15

  apply-patches:
    name: Apply Patches (ReSukiSU + NoMount)
    runs-on: ubuntu-latest
    
    steps:
      - name: Fetch NoMount Repository
        run: |
          echo "Cloning NoMount..."
          # Repository: https://github.com/maxsteeel/nomount
          git clone --branch dev https://github.com/maxsteeel/nomount.git nomount_patch
          
      - name: Fetch ReSukiSU Repository
        run: |
          echo "Cloning ReSukiSU..."
          # Repository: https://github.com/ReSukiSU/ReSukiSU
          git clone https://github.com/ReSukiSU/ReSukiSU.git resukisu_patches
```

---

## 4️⃣ scripts/build_kernel.sh

**Location:** `scripts/build_kernel.sh`  
**Purpose:** Build script with comments showing repo sources

```bash
#!/bin/bash

# Random Joke Generator Files (from this repository)
# Repository: https://github.com/SSS1981-op/OnePlus_ReSukiSU_SUSFS

# External Repositories
# Kernel: https://github.com/OnePlusOSS/android_kernel_oneplus_sm8550
# NoMount: https://github.com/maxsteeel/nomount
# ReSukiSU: https://github.com/ReSukiSU/ReSukiSU

# Step 1: Fetch OnePlus kernel
fetch_kernel() {
  log_info "Fetching OnePlus kernel from https://github.com/OnePlusOSS/android_kernel_oneplus_sm8550"
  git clone https://github.com/OnePlusOSS/android_kernel_oneplus_sm8550.git kernel_source
}

# Step 2: Fetch NoMount patches
fetch_nomount() {
  log_info "Fetching NoMount from https://github.com/maxsteeel/nomount (dev branch)"
  git clone --branch dev https://github.com/maxsteeel/nomount.git nomount_patch
}

# Step 3: Fetch ReSukiSU patches
fetch_resukisu() {
  log_info "Fetching ReSukiSU from https://github.com/ReSukiSU/ReSukiSU"
  git clone https://github.com/ReSukiSU/ReSukiSU.git resukisu_patches
}
```

---

## 5️⃣ docs/SETUP.md

**Location:** `docs/SETUP.md`  
**Purpose:** Initial setup guide with all repository links

```markdown
# Initial Setup Guide

## Prerequisites

Ensure you have the following installed:
- Git
- Build tools (gcc, make, etc.)
- Android development tools

## Repository URLs

Keep these bookmarks handy:

### Main Repositories
- Your fork: https://github.com/SSS1981-op/OnePlus_ReSukiSU_SUSFS
- OnePlus Kernel: https://github.com/OnePlusOSS/android_kernel_oneplus_sm8550
- ReSukiSU: https://github.com/ReSukiSU/ReSukiSU
- NoMount: https://github.com/maxsteeel/nomount

### Upstream Sources
- KernelSU: https://github.com/tiann/KernelSU
- OnePlus OSS: https://github.com/OnePlusOSS

## Step 1: Clone Your Repository

```bash
git clone https://github.com/SSS1981-op/OnePlus_ReSukiSU_SUSFS.git
cd OnePlus_ReSukiSU_SUSFS
```

## Step 2: Run the Build Script

The script automatically fetches from:
- https://github.com/OnePlusOSS/android_kernel_oneplus_sm8550
- https://github.com/maxsteeel/nomount (dev branch)
- https://github.com/ReSukiSU/ReSukiSU

```bash
./scripts/build_kernel.sh
```

## Troubleshooting

**Can't find OnePlus kernel?**
- Try: https://github.com/OnePlusOSS

**NoMount patch failing?**
- Check: https://github.com/maxsteeel/nomount/tree/master/kernel/patches

**ReSukiSU issues?**
- Visit: https://github.com/ReSukiSU/ReSukiSU/issues
```

---

## 6️⃣ docs/CONTRIBUTORS.md

**Location:** `docs/CONTRIBUTORS.md`  
**Purpose:** Credit upstream projects

```markdown
# Contributors & Credits

## This Project
- **Repository**: https://github.com/SSS1981-op/OnePlus_ReSukiSU_SUSFS
- **Maintainer**: @SSS1981-op

## Upstream Projects

### 1. OnePlus Kernel
- **Repository**: https://github.com/OnePlusOSS/android_kernel_oneplus_sm8550
- **Owner**: @OnePlusOSS
- **Purpose**: Base Linux kernel for OnePlus devices
- **License**: GNU General Public License v2.0

### 2. ReSukiSU
- **Repository**: https://github.com/ReSukiSU/ReSukiSU
- **Fork of**: KernelSU
- **Purpose**: Root solution with SUSFS integration
- **Features**: File hiding, permission grants, systemless modifications
- **License**: GPL-3.0

### 3. NoMount
- **Repository**: https://github.com/maxsteeel/nomount
- **Author**: @maxsteeel
- **Purpose**: VFS-based file injection without mounting
- **Features**: Path redirection, invisible modifications, banking app bypass
- **License**: GPL-3.0

### 4. KernelSU
- **Repository**: https://github.com/tiann/KernelSU
- **Author**: @tiann
- **Purpose**: Kernel-level root solution (original)
- **License**: GPL-3.0

## Community Contributors
- **XDA Developers**: Forum support and development tools
- **WildKernels**: OnePlus kernel development reference
- **Sukisu Project**: Related development work

## How to Contribute

1. **Report Issues**: Use GitHub Issues in this repository
2. **Upstream Issues**: Report bugs to respective projects:
   - OnePlus: https://github.com/OnePlusOSS
   - ReSukiSU: https://github.com/ReSukiSU/ReSukiSU/issues
   - NoMount: https://github.com/maxsteeel/nomount/issues
   - KernelSU: https://github.com/tiann/KernelSU/issues

3. **Create Pull Requests**: Follow the guidelines in CONTRIBUTING.md

## License

This project and its documentation are licensed under GPL-3.0 to match upstream projects.

See LICENSE file for details.
```

---

## 7️⃣ docs/TROUBLESHOOTING.md

**Location:** `docs/TROUBLESHOOTING.md`  
**Purpose:** Common issues with links to upstream solutions

```markdown
# Troubleshooting Guide

## Common Issues & Solutions

### Issue: Can't find OnePlus kernel repository

**Solution:**
1. Check if the repository is available: https://github.com/OnePlusOSS/android_kernel_oneplus_sm8550
2. Try the fallback repository: https://github.com/OnePlusOSS/android_kernel_oneplus_sm8650
3. Visit OnePlus OSS: https://github.com/OnePlusOSS for other kernel versions

### Issue: NoMount patch fails to apply

**Solution:**
1. Check patch compatibility: https://github.com/maxsteeel/nomount/tree/master/kernel/patches
2. Read INTEGRATION guide: https://github.com/maxsteeel/nomount/blob/master/kernel/INTEGRATION.md
3. Report issue: https://github.com/maxsteeel/nomount/issues

### Issue: ReSukiSU build fails

**Solution:**
1. Check ReSukiSU issues: https://github.com/ReSukiSU/ReSukiSU/issues
2. Check KernelSU base: https://github.com/tiann/KernelSU
3. See KernelSU docs: https://kernelsu.org

### Issue: Kernel build error

**Solution:**
1. Check OnePlus documentation: https://opensource.oneplus.com/
2. Verify kernel version: https://github.com/OnePlusOSS/android_kernel_oneplus_sm8550/tags
3. Check build requirements in NOMOUNT_BUILD_GUIDE.md

## Getting Help

1. **This Project Issues**: https://github.com/SSS1981-op/OnePlus_ReSukiSU_SUSFS/issues
2. **Upstream Issues**:
   - OnePlus: https://github.com/OnePlusOSS/issues
   - ReSukiSU: https://github.com/ReSukiSU/ReSukiSU/issues
   - NoMount: https://github.com/maxsteeel/nomount/issues
   - KernelSU: https://github.com/tiann/KernelSU/issues

3. **Community Forums**:
   - XDA Developers: https://forum.xda-developers.com/
   - OnePlus Forums: https://forums.oneplus.com/

## Documentation Links

- [Build Guide](../NOMOUNT_BUILD_GUIDE.md)
- [Setup Instructions](./SETUP.md)
- [Contributors](./CONTRIBUTORS.md)
```

---

## 8️⃣ .github/ISSUE_TEMPLATE/bug_report.md

**Location:** `.github/ISSUE_TEMPLATE/bug_report.md`  
**Purpose:** Issue template with relevant repository links

```markdown
---
name: Bug Report
about: Report a bug in the build process or kernel
title: "[BUG] "
labels: bug
assignees: ''

---

## Bug Description
<!-- Describe the bug clearly -->

## Affected Component
- [ ] OnePlus Kernel (https://github.com/OnePlusOSS/android_kernel_oneplus_sm8550)
- [ ] NoMount patches (https://github.com/maxsteeel/nomount)
- [ ] ReSukiSU patches (https://github.com/ReSukiSU/ReSukiSU)
- [ ] Build script
- [ ] Other

## Steps to Reproduce
1. Step 1
2. Step 2

## Expected Behavior

## Actual Behavior

## Environment
- OS: 
- Kernel version: 
- Script version: 

## Relevant Links
- Related upstream issue: 
- Commit: 
- Documentation: 

## Additional Context
```

---

## 📊 Summary Table

| Location | Content | Repository Links | Purpose |
|----------|---------|------------------|---------|
| `README.md` | Main overview | 4+ links in table | Entry point |
| `NOMOUNT_BUILD_GUIDE.md` | Complete guide | Inline links in every section | Comprehensive reference |
| `.github/workflows/*.yml` | CI/CD workflows | Comments with URLs | Automated building |
| `scripts/*.sh` | Build scripts | Comments with clone URLs | Automatic fetching |
| `docs/SETUP.md` | Initial setup | Bookmarked links | Getting started |
| `docs/CONTRIBUTORS.md` | Credits | Complete repository URLs | Attribution |
| `docs/TROUBLESHOOTING.md` | Help & support | Issue tracker links | Problem solving |
| `.github/ISSUE_TEMPLATE/` | Bug reports | Checkboxes for components | Community support |

---

## 🎯 Best Practices

✅ **DO:**
- Link to specific commits/branches when relevant
- Include full GitHub URLs for clarity
- Keep links updated when repositories change
- Document the purpose of each link
- Use markdown table format for organization
- Add links in comments within code files

❌ **DON'T:**
- Use shortened URLs (they break easily)
- Put unformatted URLs in the middle of sentences
- Forget to update links when repos move
- Link to URLs that require authentication
- Mix relative and absolute paths inconsistently

---

## 🔗 Quick Reference

```
Your Repository:
https://github.com/SSS1981-op/OnePlus_ReSukiSU_SUSFS

External Repositories:
- OnePlus: https://github.com/OnePlusOSS/android_kernel_oneplus_sm8550
- ReSukiSU: https://github.com/ReSukiSU/ReSukiSU
- NoMount: https://github.com/maxsteeel/nomount
- KernelSU: https://github.com/tiann/KernelSU

Official Resources:
- OnePlus OSS: https://opensource.oneplus.com/
- KernelSU Docs: https://kernelsu.org
- ReSukiSU Docs: https://ReSukiSU.github.io
```

