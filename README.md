# Backup
Backup is a basic wrapper to make borgmatic more convenient, it is currently only for full whole-system backups and has few features as it is in early development. It currently expects your repo to be in ~/backup/repo, the excluding is currently permanent only. The backup names are always date-based.
The options to use your own repo name, choose the backup directory instead of always root, have session-specific as well as permanent excludes, automatic backups available if wanted, your own filename if wanted & automatic descriptions of the differences of each backup in files are all in beta and with little development currently.

# Usage
to exclude a specific directory permanently the syntax is:

```bash
backup --exclude '/dir'
```
to remove an exclude permanently the syntax is:
```bash
backup --dont-exclude '/dir'
```
to list the excludes the syntax is:
```bash
backup --list-excludes
```
then to actually backup syntax is:
```bash
backup
```
when it backups, it currently always gives you an automatic filename based on date, an example is provided below:
```bash
1st-of-april
```
# Licensing
This project is licensed under the Mozilla Public License V. 2.0. Any modified version of my iwmenu.c file that gets distributed must remain under this license and stay open-source due to legal rights. Please see the LICENSE file or https://mozilla.org/MPL/2.0/. for the full terms. Other users are free to modify and distribute this file if they follow the MPL 2.0 licensing agreements.
