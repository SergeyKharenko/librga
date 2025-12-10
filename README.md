
---

## **Introduction**

This repository is a streamlined fork of Rockchip’s official **librga** userspace driver.

The goal of this fork is to make **librga easier to install, integrate, and consume** on typical aarch64 Linux systems.
Compared to the upstream project, non-essential directories such as `docs/`, `toolchains/`, and `tools/` have been removed to keep the repository compact and focused on practical deployment.

A key improvement in this fork is the inclusion of a **`librga.pc`** file for aarch64, allowing `pkg-config` to automatically detect and link against librga without manual configuration.

For users who simply want a clean “drop-in” installation, this fork also provides a minimal set of installation steps for headers, libraries, and udev rules.

---

## **Install**

The instructions below target **aarch64 Linux** systems (e.g., Debian/Ubuntu on ARM64).
Other architectures can be added in the future.

> **Note:** The commands below require root privileges. Run them with `sudo` or as `root`.

### **1. Install headers**

```sh
sudo install -d /usr/include/rga
sudo cp -a include/* /usr/include/rga/
```

### **2. Install aarch64 libraries**

```sh
sudo install -d /usr/lib/aarch64-linux-gnu
sudo cp -a libs/Linux/gcc-aarch64/* /usr/lib/aarch64-linux-gnu/
```

### **3. Install the pkg-config file**

```sh
sudo install -d /usr/lib/aarch64-linux-gnu/pkgconfig
sudo install -m 0644 pkgconfig/aarch64/librga.pc \
    /usr/lib/aarch64-linux-gnu/pkgconfig/librga.pc
```

You can verify the installation with:

```sh
pkg-config --cflags --libs librga
```

### **4. Install udev rules (optional but recommended)**

```sh
sudo install -m 0644 50-rga.rules /etc/udev/rules.d/50-rga.rules
sudo udevadm control --reload-rules
sudo udevadm trigger
```

After completing these steps, **librga** should be available system-wide, and `pkg-config` will be able to locate it automatically.

---
