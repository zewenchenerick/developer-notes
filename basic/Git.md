

## Foundation

### Why Version Control System
- Track History
- Collaborate with others

### Types of Version Control System
- Centralized
- Distributed




## Creating Snapshots
### Staging area
The **staging area** in Git also known as the **index** is an intermediate space where you can **prepare and review changes** before finalizing them with a commit. 
There are some key features which is useful:
- **Selective commit**
- **Review changes**
- **Logical Grouping**: *create logical commit by staging relative changes.*

#### Add file into staging area
```bash
git add file1.js # add file into staging area
```

#### Commit
```bash
git commit -m 'first commit' 
# every commit git store fill content not diff
```

#### Add and commit Together
```bash
git commit -ma 'refactor code.' # add and commit simultaneously 
```
> **Noted**: This method is not recommended 

#### Remove file from Staging area
```bash
git rm --cached -r bin/ 
# -r stand for recursive (there multiple files under the path)
```


## Browsing History
