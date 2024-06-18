# Test Data for the `hypermri` package

> _Current Version: v0.1.0_

## How to Add Files

There exists one folder for each sequence to be tested. Inside the `bruker` directory, add a new folder named after the sequence. In this folder, you can put the BrukerExp scan folders/data.

Next to the BrukerExp folders, general study-related files are currently handled as follows:

|  Type  |          Name              |  Keep?  |
|--------|----------------------------|---------|
| Folder | AdjResults                 | No      |
| Folder | Mapshim                    | No      |
| File   | AdjStatePerStudy           | No      |
| File   | ScanProgram.scanProgram    | No      |
| File   | subject                    | **Yes** |
| File   | ResultState                | No      |

---

## Implementation Details

### Steps to Create This Repo

1. **Initialize Git LFS**

```bash
❯ git lfs install
```

2. **Create Config File to List Binary Files to Track**

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
❯ git commit -m "Configure Git LFS to track fid and 2dseq files"
❯ git push origin main
```

### Changelog Generation

The changelog is automatically generated from the commit messages using [git-cliff](https://git-cliff.org).

Git-cliff is configured in the `./cliff.toml` file and is integrated into GitHub actions via the `.github/workflows/gitcliff.yml` file.

Depending on your commit message, the commit will appear in the changelog based on these regex patterns:

```json
# regex for parsing and grouping commits
commit_parsers = [
    { message = "^.*: add", group = "Added" },
    { message = "^.*: support", group = "Added" },
    { message = "^.*: remove", group = "Removed" },
    { message = "^.*: delete", group = "Removed" },
    { message = "^test", group = "Fixed" },
    { message = "^fix", group = "Fixed" },
    { message = "^.*: fix", group = "Fixed" },
    { message = "^.*", group = "Changed" },
]
```

### Version Bumping

Version bumping is semi-automatic. [Git-cliff](https://git-cliff.org) suggests the correct version, but you must manually create a tag and generate a dedicated commit. The workflow is as follows:

1. **Get Suggested Version**

```bash
❯ git cliff --bumped-version
v0.1.0
```

Update the version in the `README.md` file to this newly suggested version (in this case v0.1.0).

2. **Commit and Tag the New Version**

```bash
❯ git add README.md
❯ git commit -m "Bumped version to v0.1.0"
❯ git tag v0.1.0
❯ git push origin main --tags
```

3. **Pull the Latest Changes**

The changelog and version are now automatically updated. To avoid merge conflicts, pull these changes (this might take 1-2 minutes):

```bash
❯ git pull
```