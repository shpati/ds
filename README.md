# ds — Disk Space at a Glance

A clean, colourful terminal tool that shows used, free, and total space for every real drive on your machine.

```
  💾  Disk Space Report
  Mount                           Total       Used       Free   Usage                           Used%
  ──────────────────────────────────────────────────────────────────────────────────────────────────────
  /                            926.4 GB   905.8 GB    20.6 GB   [█████████████████████████████░]  97%
  /Volumes/PSSD                  1.9 TB     1.9 TB     8.3 GB   [█████████████████████████████░]  99%
  ──────────────────────────────────────────────────────────────────────────────────────────────────────
  2 drive(s) found  ·  2026-03-29 12:10:44
```

## Features

- Works on **macOS** and **Linux** with no OS detection logic
- Skips synthetic/virtual volumes (APFS sub-volumes, loop devices, snap mounts, boot partitions)
- Colour-coded usage bars — green → yellow → red as disks fill up
- Human-readable sizes (KB / MB / GB / TB)
- No dependencies beyond `bash`, `df`, and `awk`

## Installation

```bash
# Clone or download, then make it executable
chmod +x ds

# Run from anywhere by moving it onto your PATH
mv ds /usr/local/bin/ds
```

## Usage

```bash
ds
```

That's it — no flags, no arguments.

## Colour coding

| Colour    | Meaning        |
| --------- | -------------- |
| 🟢 Green  | Under 70% full |
| 🟡 Yellow | 70–89% full    |
| 🔴 Red    | 90%+ full      |

## Compatibility

| Platform                      | Status          |
| ----------------------------- | --------------- |
| macOS (Intel & Apple Silicon) | ✅               |
| Linux                         | ✅               |
| Windows (Git Bash / MSYS2)    | ❌ not supported |

## How it works

`ds` runs `df -Pk` (POSIX format, 1 KB blocks) and filters the output with `awk` to keep only rows where:

- the filesystem path starts with `/dev/` (real block devices only)
- the mount point is not under `/System/Volumes/` (excludes macOS APFS sub-volumes)
- the mount point is not a loop device, snap mount, or boot partition

This single filter works identically on macOS and Linux without any platform detection.

## License

MIT
