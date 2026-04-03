# Backup
Backup is a bash wrapper for borg to make creating and managing backups more convenient. It supports backing up any directory (not just root), per-repo encryption, custom or date-based archive names, permanent exclude lists, automatic changelog generation between backups, and passphrase management across all repos.

This branch targets borg 1.x. For borg 2.x with full features, switch to the main branch. Note that `--password` on this branch cannot convert unencrypted repos to encrypted ones — that requires `borg transfer` which is only available in borg 2.x.

# Dependencies
- `borg` 1.x
- `python3` (used for parsing repo encryption info)
- `sudo`

# Usage

Run a backup:

    backup

You will be prompted for the directory to back up, whether to use the default date-based archive name, and the repo passphrase if one is set. On the first backup of a directory, you will also be prompted to set a passphrase for the new repo (leave blank for no encryption).

The default archive name is date-based, for example:

    Monday-7th-of-april-25

Set the base repo path permanently:

    backup --repo <path>
    backup --repo=<path>

Add a permanent exclude:

    backup --exclude '/path/to/dir'

Remove a permanent exclude:

    backup --dont-exclude '/path/to/dir'

List all permanent excludes:

    backup --list-excludes

Change the passphrase on all encrypted repos:

    backup --password <newpassphrase>
    backup --password=<newpassphrase>

You will be prompted for the current passphrase. Press enter if repos are currently unencrypted. Unencrypted repos will be skipped — converting an unencrypted repo to an encrypted one is not supported on this branch.

# Repo structure
Repos are organised under the base repo path by source directory. For example:
- A backup of `/` goes to `<base>/full-system-backup/`
- A backup of `/home` goes to `<base>/home/`
- A backup of `~/.config` goes to `<base>/home/<user>/.config/`

# Changelog
After each backup (from the second backup of a given repo onwards), a `backup-changelog.txt` file is automatically created and appended to inside the repo directory. It records the archive name, date, number of files added/removed/modified, new and removed systemd services, and modified config files.

# Default excludes
The following paths are always excluded regardless of the permanent exclude list:
`/dev/*`, `/proc/*`, `/sys/*`, `/tmp/*`, `/run/*`, `/mnt/*`, `/media/*`, `/var/cache/*`, `/var/tmp/*`, `~/.cache/*`

# Config files
| File | Purpose |
|------|---------|
| `~/.config/borg-backup/excludes` | Permanent exclude list |
| `~/.config/borg-backup/repo` | Stored base repo path |

# Licensing
This project is licensed under the Mozilla Public License v2.0. Any modified version of files in this project that gets distributed must remain under this license and stay open-source. See the LICENSE file or https://mozilla.org/MPL/2.0/ for the full terms.
