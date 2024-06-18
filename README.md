# Test Data for the `hypermri` Package

> _Current Version: v0.1.0_

## 1. Adding Test Data

To add new test data, follow these steps:

1. Inside the `bruker` directory, create a new folder named after the sequence.
2. Place the BrukerExp scan folders/data in this new folder.

### 1.1 General Study-Related Files Handling

The following table details which general study-related files should be kept or discarded:

|  Type  |          Name              |  Keep?  |
|--------|----------------------------|---------|
| Folder | AdjResults                 | No      |
| Folder | Mapshim                    | No      |
| File   | AdjStatePerStudy           | No      |
| File   | ScanProgram.scanProgram    | No      |
| File   | subject                    | **Yes** |
| File   | ResultState                | No      |

### 1.2 Example - Adding Test Data

1. Create a folder inside `./bruker`, name it after the sequence, and place your test data in it.
2. Commit and push your changes:

    ```bash
    ❯ git add .
    ❯ git commit -m "add: Added test data for my sequence"
    ❯ git push
    ```

3. Verify the changelog update:

    After 1-2 minutes, pull the changes and check the `CHANGELOG.md` file to ensure the update was logged correctly.

---
## 2. More Details

### 2.1 Conventional Commits and Changelog Generation

Commit messages should follow these prefixes to categorize changes in the changelog:

| Commit Message Prefix |  Changelog Section  |
|-----------------------|---------------------|
| `add:`                |  Added              |
| `remove:`             |  Removed            |
| `fix:`                |  Fixed              |
| `change:`             |  Changed            |
| _other_               |  Other              |

This format is based on the [Conventional Commits specification](https://www.conventionalcommits.org/en/v1.0.0/). The changelog is generated using [git-cliff](https://git-cliff.org), configured via `./cliff.toml`, and integrated into our GitHub Actions workflow (`.github/workflows/gitcliff.yml`).

### 2.2 Version Bumping

Version bumping is semi-automatic. Follow these steps to update the version:

1. **Get Suggested Version**

    ```bash
    ❯ git cliff --bumped-version
    v0.1.0
    ```

2. **Update Version and Commit**

    Update the version in the `README.md` file and commit the change:

    ```bash
    ❯ git add README.md
    ❯ git commit -m "Bumped version to v0.1.0"
    ❯ git tag v0.1.0
    ❯ git push origin main --tags
    ```

3. **Pull the Latest Changes**

    To avoid merge conflicts, pull the latest changes:

    ```bash
    ❯ git pull
    ```

The changelog and version are now automatically updated.

### 2.3 Initial Setup

1. **Initialize Git LFS**

    ```bash
    ❯ git lfs install
    ```

2. **Create Config File for Binary Files**

    ```bash
    ❯ touch .gitattributes
    ```

3. **Track Binary Files Using Git LFS**

    Add the following lines to `.gitattributes` to track specific binary file types:

    ```
    fid filter=lfs diff=lfs merge=lfs -text
    2dseq filter=lfs diff=lfs merge=lfs -text
    *.bin filter=lfs diff=lfs merge=lfs -text
    *.asc filter=lfs diff=lfs merge=lfs -text
    *.scanProgram filter=lfs diff=lfs merge=lfs -text
    ```

4. **Commit and Push Changes**

    ```bash
    ❯ git add -A
    ❯ git commit -m "Configure Git LFS to track e.g., fid, 2dseq files"
    ❯ git push origin main
    ```
