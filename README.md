<h1 align="center">
Cargo Backup
</h1>
<p align="center">
	<img src="https://img.shields.io/crates/v/cargo-backup" />
	<img src="https://img.shields.io/crates/d/cargo-backup" />
	<img src="https://img.shields.io/crates/l/cargo-backup" />
</p>

<p align="center">
	Backup your installed cargo packages with full metadata and binary validation
</p>


# installation
```sh
cargo install cargo-backup
```

# Usage
## Backup
```sh
cargo backup <args>
```
### Arguments
* `--out | -o` - The output file where the backup will be written to. default `backup.json`

The backup command captures the following package information:
- Package name and version
- Build profile (release, debug, custom)
- Target architecture (e.g., aarch64-apple-darwin)
- Enabled features
- Version requirements
- Installed binaries
- Source path (for path-based packages)

All package types are supported: registry packages, path-based packages, and git-based packages.

## Restore
```sh
cargo restore --backup path/to/backup <args>
```
### Arguments
* `--backup | -b` - The backup file. *required*
* `--skip-install | -i` - Skips the installation of new packages.
* `--skip-update | -u` - Skips the packages to update.
* `--skip-remove | -r` - Skips the removal of packages not found in the backup.
* `--yes | -y` - Skips the confirmation prompt.

The restore command validates that binaries actually exist in `~/.cargo/bin/`. If binaries are missing for packages listed in `.crates2.json`, they will be marked for reinstallation.

Path-based packages are reinstalled using `--path <directory>`. Registry packages use version-based installation. Git-based packages are reinstalled using `--git <url>`. 

## Sync
Requires a Github account.
```sh
cargo sync <sub-command> <args>
```

### Login
```sh
cargo sync login <args>
```

#### Arguments
* `--force | -f` - Ignores the current Credentials.

### Push
Either push a new backup or Updates the old one.
```sh
cargo sync push <args>
```

### Pull
Pulls the backup from the gist repository.
**A valid gist id needs to be set for this.**
```sh
cargo sync pull <args>
```

#### Arguments
* `--skip-install | -i` - Skips the installation of new packages.
* `--skip-update | -u` - Skips the packages to update.
* `--skip-remove | -r` - Skips the removal of packages not found in the backup.
* `--yes | -y` - Skips the confirmation prompt. 

### set-id
```sh
cargo sync set-id <gist-id>
```

# Features
- Binary validation during restore ensures packages are actually installed, not just registered
- Path-based package support for local development tools
- Git-based package support for packages installed from git repositories
- Full metadata preservation (profile, target, features, bins)
- Support for all git protocols (HTTPS, HTTP, SSH)
- Skip confirmation prompts for automation and scripting
- Automatic sync message when system is already in sync with backup

# License
[MIT](https://choosealicense.com/licenses/mit/)
