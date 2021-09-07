# Git & GitHub

## Notes

### Configuration

Local configuration

```bash
# Set default editor when opening config files to vim
# [--global] is optional to switch from local setting to global setting
git config [--global] core.editor "vim"
# Open git config file
git config -e [--global] 
```

Config GitHub

```bash

```

### Get started

```bash
# Initialize a local repo
git init <directory>
# Clone from a remote repo
git clone git@github.com:fsliurujie/test.git         # --SSH
git clone git://github.com/fsliurujie/test.git       # --GIT
git clone https://github.com/fsliurujie/test.git     # --HTTPS
```

### File Operation

```bash
# Add
git add <file1> <file2> ...          # 添加多个文件
git add <dir>                        # 添加目录

# Remove
git rm <file> # 从工作区和暂存区删除
git rm --cached <file> # 仅从暂存区删除 
git rm -f <file> # 强制删除
git rm -r <dir> # 递归删除目录

# Move
git mv <file> <newfile>
git mv -f <file> <newfile>

# Commit
git commit -m <message>                        # 提交暂存区所有文件到本地仓库 
git commit <file1> <file2> ... -m <message>    # 提交暂存区指定文件到本地仓库
git commit -a                                  # 等价于git add + git commit
```

### Branch

```bash
git branch 					# list local branches
git branch <branchname> 	# create branch 
git branch -b <branchname> 	# create and switch to branch
git branch -d <branchname> 	# delete branch
git checkout <branchname> 	# switch to branch
git merge 					# merge branches
```

### Log

```bash
```



