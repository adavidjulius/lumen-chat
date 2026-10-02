# Full Report: kcclab.mitindia.edu (192.168.1.45)

**Generated:** 2026-09-11
**Method:** SSH via paramiko (password auth) as user `ct2026503586`
**Connection:** ✅ Successful

---

## 1. Connection & Identity

| Item | Value |
|---|---|
| Host (IP) | 192.168.1.45 |
| Hostname | kcclab.mitindia.edu |
| SSH Port | 22 (OpenSSH) |
| Login User | ct2026503586 (uid 1734, gid 1738) |
| Home Directory | /home/ct2026503586 |
| Auth Mode | Password (worked) |
| Shell | /bin/bash |
| Locale | en_IN.UTF-8 |
| Client IP seen by server | 192.168.195.118 |

---

## 2. OS / Platform

| Item | Value |
|---|---|
| OS | CentOS Stream 10 (Coughlan) |
| Kernel | Linux 6.12.0-257.el10.x86_64 |
| Arch | x86-64 |
| Package base | RPM (1813 packages installed) |
| SELinux | **Enforcing** |
| Firewall | firewalld **active** |
| Install date | 13 Aug 2026 |
| Uptime | 14 days, 6+ hours |

This is an enterprise-grade RHEL 10-family server with SELinux enforcing and firewalld active — a properly hardened multi-user environment.

---

## 3. Hardware

| Component | Detail |
|---|---|
| Vendor/Model | FUJITSU PRIMERGY RX2540 M1 (rack server) |
| Firmware | V5.0.0.9 R1.16.0 (D3289-A1x), dated 2015-02-05 |
| CPU | 2× Intel Xeon E5-2630 v3 @ 2.40 GHz (8 cores each, HT on) = **32 logical CPUs** |
| CPU cache | 40 MiB L3, 4 MiB L2, 512 KiB L1d/i per core |
| NUMA | 2 nodes |
| Virtualization | VT-x (hardware virtualization capable) |
| RAM | **125 GiB total** (~99 GiB available, 26 GiB used) |
| Swap | 31 GiB (unused) |
| GPU | Matrox MGA G200e server VGA only — **no GPU compute** (no NVIDIA) |

---

## 4. Storage

| Mount | Device | Size | Used | Use% |
|---|---|---|---|---|
| / | /dev/mapper/cs-root (LVM on sda3) | 70 GB (xfs) | 21 GB | 30% |
| /home | /dev/mapper/cs-home | 3.2 TB (xfs) | 63 GB | 2% |
| /boot | /dev/sda2 | 960 MB (xfs) | 607 MB | 64% |
| /boot/efi | /dev/sda1 | 599 MB (vfat) | 8.9 MB | 2% |
| swap | /dev/mapper/cs-swap | 32 GB | — | — |

Raw disk: `sda` = 3.3 TB. Inode usage <1%. Plenty of free space in /home. Per-user quota tooling (`repquota`, `xfs_quota`) is **not accessible** to a normal user, so it is unenforced from your side.

---

## 5. Network

| Item | Value |
|---|---|
| Primary NIC | eno1 — 192.168.1.45/24 |
| Secondary NIC | eno2 — DOWN |
| Gateway | 192.168.1.1 |
| DNS | 8.8.8.8, 4.2.2.2 (search mitindia.edu) |
| Public egress IP | 14.139.190.103 (MITT / Anna University range) |
| Outbound ping | Works (0% loss to 8.8.8.8, ~2.3 ms) |
| Listening ports | :80 (nginx), :8000 (JupyterHub), :8081, :8001, :44321/44339/44375 (local only) |

---

## 6. Software Stack

### Languages / Compilers
- **Python** 3.12.13 (`/usr/bin/python3`) + pip 23.3.2
- **GCC/G++** 14.4.1 (Red Hat) — full C/C++ toolchain
- **Node.js** v22.23.1 + npm 10.9.8
- **Perl**
- **GNU Make** 4.4.1, **autoconf**, **gdb**, **valgrind**, **strace**
- No Java, Go, Rust, .NET, PHP, Ruby, R, Julia found.

### Containers
- **Podman 6.1.0**, rootless = **true** ✅ (verified by running an alpine container successfully)

### Web / Servers
- **nginx** (running, serving on :80, `kcclab.mitindia.edu` vhost → /var/www/html/kcclab)
- **httpd** (Apache) installed but not the active web front-end
- **JupyterHub** running since 2026-09-08, bound to `0.0.0.0:8000`, PAM auth, `allow_all=True`, default_url `/lab`, admins: admin, kccadmin, shutdown_on_logout=True

### Dev Tools Available
`curl`, `wget`, `git` 2.52.0, `scp`, `rsync`, `tar`, `gzip`, `zip`/`unzip`, `tmux`, `iostat`, `vmstat`, `sar`, `free`, `dig`, `nslookup`, `netstat`, `ss`, `lsof`, `strace`, `gdb`, `valgrind`, `vim`, `vi`, `nano`, `code` (VS Code CLI)

### Python packages of interest
`jupyter_*` (full Jupyter stack), `ipykernel` 7.3, `ipython` 9.16, `ansible-core` 2.16.19, `httpx`, `cryptography`, `certipy`, `dnf`, `cockpit` bindings.

### System services running
GDM (desktop), CUPS, chronyd, firewalld, sshd, jupyterhub, nginx, irqbalance, PCP (pmcd/pmie/pmlogger — performance metrics), smartd, auditd, rsyslog, avahi, NetworkManager, ModemManager, accounts-daemon, rtkit.

---

## 7. Privileges & Constraints

| Check | Result |
|---|---|
| sudo (non-interactive) | ❌ Requires password — you do **not** have passwordless sudo |
| Root access | ❌ No |
| Group memberships | Only own primary group (1738) |
| Read /etc/ssh/sshd_config | ❌ Permission denied |
| Read /etc/nginx/nginx.conf | ✅ Yes (world-readable) |
| Read /etc/jupyterhub/jupyterhub_config.py | ✅ Yes (world-readable) |
| Install system RPMs | ❌ No (needs root) |
| Rootless podman | ✅ Yes — you can build/run containers |
| SELinux | Enforcing (may affect some files/ports) |

### Running processes on the box
Shared lab workload: many `./a.out` processes owned by `robo202*`, `rp20265*`, `aero202*` users each consuming ~95–99% CPU. **Load average ≈ 37** on 32 cores — the machine is heavily busy with other students' workloads. Logged-in users: several `ct2026*` accounts plus `kccadmin` on tty2.

---

## 8. What You Can Actually Do (Capability Summary)

### ✅ Fully supported
- Compile & run C/C++ (`gcc`/`g++`), e.g. `gcc prog.c -o prog && ./prog`
- Write & run Python 3.12 scripts; use pip with `--user` (system installs need root)
- Run Node.js 22 apps/scripts
- Use Git, tmux, rsync, scp for development workflows
- Build/run OCI containers **rootless** with Podman (pull from Docker Hub, etc.)
- Full internet access (curl/wget/ping outbound)
- Access JupyterLab via `http://kcclab.mitindia.edu:8000` (or `http://192.168.1.45:8000`) with your PAM credentials — kernel lives in /home, so your notebooks persist
- Access the lab web server at `http://kcclab.mitindia.edu/`
- ~3.2 TB of /home space, subject only to underlying FS capacity (no enforced quota seen)
- Run long jobs via `tmux`/`nohup` (mandatory because of ssh session limits)

### ⚠️ Limited / caveats
- **No sudo** — cannot install system packages, edit /etc, manage services, or open privileged ports
- **No GPU** — CPU-only workloads; no CUDA/tensor training
- **Shared, busy node** — load ~37; your jobs compete with dozens of other users' `a.out` processes. Be a good citizen: use `nice`, limit threads, and use `tmux`
- **SELinux enforcing + firewalld active** — some network binds and file ops may be blocked; local ports >1024 are fine
- **SSH password auth** — consider generating an ed25519 key pair and adding `~/.ssh/authorized_keys` for convenience (you can, since you own your home)

### ❌ Not possible without admin
- Installing RPM packages (`dnf install`) or Python system packages
- Changing sshd/nginx/firewalld configuration
- Rebooting, mounting, or creating users
- Accessing other users' files

---

## 9. Quick-start Cheatsheet

```bash
# SSH in
ssh ct2026503586@192.168.1.45

# Start a persistent session
tmux new -s work

# C/C++ workflow
gcc -O2 -o prog prog.c && ./prog

# Python (user-site installs)
python3 -m pip install --user <pkg>

# Rootless container
podman run --rm -it docker.io/library/alpine:3.20 sh

# JupyterLab (from your laptop browser)
http://kcclab.mitindia.edu:8000   ->  login with your PAM user/password
```

---

## 10. Recommendations

1. **Add an SSH key** to `~/.ssh/authorized_keys` for passwordless login.
2. **Always run heavy jobs inside `tmux`** — a dropped SSH session will otherwise kill them.
3. **Nice your long-running processes** (`nice -n 10 ...`) given the machine is loaded at ~37 on 32 cores.
4. **Use Podman rootless** for isolated dev environments — you cannot install system tooling, but you can ship anything in a container.
5. **Keep work in `/home/ct2026503586/`** — that's your only writable persistent space (root FS is small at 70 GB and shared).
6. **Use JupyterLab on port 8000** for interactive Python/data work; it's already wired up.
