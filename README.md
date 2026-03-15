# rtree

A fast, colorful `tree` replacement with smart pattern filtering and a live-search TUI.

## Why?

The classic `tree` command's `-P` pattern filter is misleading — it still expands every directory, just showing zero matching files inside them:

```
$ tree ~/Downloads -P "*.zip" -L 3
/home/user/Downloads
├── Amethyst
│   ├── colmap_data
│   │   ├── images
│   │   └── sparse
...
103 directories, 0 files
```

`rtree` prunes the tree to only show paths that actually lead to a match:

```
$ rtree ~/Downloads -P .zip -L 3
Downloads
├── packet_delivery_service
│   ├── resources.zip
├── Telegram Desktop
│   ├── tmp
│   │   ├── data.zip
│   │   ├── matrices.zip
│   ├── led_controller.zip
├── Godot_v4.3-stable_linux.x86_64.zip
├── linux.main.zip
...
3 directories, 40 files
```

## Install

```bash
# AUR
yay -S rtree

# From source
cargo install --path .
```

## Usage

```
rtree [OPTIONS] [PATH]
```

### Listing options

| Flag | Description |
|------|-------------|
| `-a` | Show hidden files |
| `-d` | Directories only |
| `-l` | Follow symlinks |
| `-f` | Print full paths |
| `-x` | Stay on one filesystem |
| `-L <N>` | Limit depth to N |
| `-P <PATTERN>` | Show only entries matching pattern |
| `-I <PATTERN>` | Exclude entries matching pattern |
| `--prune` | Prune empty directories |

### Sorting options

| Flag | Description |
|------|-------------|
| `-v` | Natural/version sort |
| `-t` | Sort by modification time |
| `-c` | Sort by status change time |
| `-U` | Unsorted |
| `-r` | Reverse sort order |

### File information

| Flag | Description |
|------|-------------|
| `-s` | Show file sizes |
| `-H` | Human-readable sizes |
| `-p` | Show permissions |
| `-D` | Show last modified date |

### Color

```bash
rtree --color=always   # full file-type colors
rtree --color=auto     # smart: detects piped output, busy flags (default)
rtree --color=simple   # directories and symlinks only
rtree --color=never    # no color
```

`--color=auto` (the default) will:
- Use no color when output is piped
- Use simple color when `--permissions` or `--date` are active (avoids visual noise)
- Use full color otherwise

### Output formats

```bash
rtree --json    # JSON
rtree --xml     # XML
rtree --tui     # Interactive live-search TUI
rtree --tui --search foo   # TUI with pre-filled search
```

## License

MIT
