# Test Data for the `hypermri` package

--------
**v0.1.0**
--------

## How to add files:

There exists one folder for each sequence to be tested. Inside the `bruker` directory,
add a new folder named after the sequence, in here you can put the BrukerExp folders.

Next to the BrukerExp folders, general study related files are handled as follows:


|  Type  |          Name              |  Keep?  |
|--------|----------------------------|---------|
| Folder | AdjResults                 | No      |
| Folder | Mapshim                    | No      |
| File   | AdjStatePerStudy           | No      |
| File   | ScanProgram.scanProgram    | No      |
| File   | subject                    | **Yes** |
| File   | ResultState                | No      |

---


#### Steps done to create this repo

1. Init git lfs

```bash
❯ git lfs install
```

2. Create config file to list binary files to track
```bash
❯ touch .gitattributes
```

3. Use 'git lfs track...' or inside .gitattributes write:
```
fid filter=lfs diff=lfs merge=lfs -text
2dseq filter=lfs diff=lfs merge=lfs -text
*.bin filter=lfs diff=lfs merge=lfs -text
*.asc filter=lfs diff=lfs merge=lfs -text
*.scanProgram filter=lfs diff=lfs merge=lfs -text
```

4. Commit and push
``` bash
git add -A
git commit -m "Configure Git LFS to track fid and 2dseq files"
git push origin main
```


#### Changelog 

The changelog is automatically generated from the commit messages using [git-cliff](https://git-cliff.org).

Git-cliff is configured in the `./cliff.toml` file and is integrated into GitHub actions via the `.github/workflows/gitcliff.yml` file.

Depending on your commit message, the commit will appear in the changelog:

table MISSING


#### Version Bumping

Version Bumping is done semi-automatic. While git-cliff suggests the correct version, a tag has to be manually created and a dedicated commit should be generated. The workflow goes as follows:

```bash
❯ git cliff --bumped-version
v0.1.0
```

Update version in `README.md` file to this newly suggested version (in this case v0.1.0), then:

```bash
❯ git add README.md
❯ git commit -m "Bumped version to v0.1.0"
❯ git tag v0.1.0
❯ git push origin main --tags
```