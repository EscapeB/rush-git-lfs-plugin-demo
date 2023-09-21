# rush-git-lfs-plugin-demo

## Pre-requisite
You should have [git-lfs](https://git-lfs.com/) installed in your environment.

git-lfs version should >= 3.3.0

> you can check your git-lfs version by running `git lfs version`


## Configuration
`common/config/rush-plugins/rush-git-lfs-plugin.json`
```json5
{
  "errorTips": "We use Git LFS to manage large files in our Monorepo",
  "checkPattern": {
    // key was glob pattern, value was max size in bytes
    // if value is -1, it means all files that meet glob pattern should be managed by git lfs
    "**/*.snap": -1,
    "**/*.jpg": -1,
    // default threshold value for all files.
    "**/*": 1048576
  }
}
```

## Commands


### rush git-lfs-pull
pull lfs objects for project and it's dependencies projects

```bash
# because project-a depends on project-b, lfs objects inside project-b folder will be pulled as well.
rush git-lfs-pull --to project-a
```

### rush git-lfs-check
check if committed file was correctly managed by git lfs
```bash
# should throw errors for both two files.
rush git-lfs-check --file apps/project-a/assets/lfs.snap --file apps/project-a/assets/lfs.jpg
```
Or you can automatic fix errors by adding `--fix`
```bash
# will use `git lfs track` to track these two files and created .gitattributes file in project-a's folder
rush git-lfs-check --file apps/project-a/assets/lfs.snap --file apps/project-a/assets/lfs.jpg --fix
```
