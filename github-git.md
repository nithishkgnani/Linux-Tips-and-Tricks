[Back to Readme](README.md)

### Merge issues

* If the problem is "main and master are entirely different commit histories.", the following will work

```bash
git checkout master   
git branch main master -f    
git checkout main  
git push origin main -f 
```

[source](https://stackoverflow.com/a/66527784)

* Make an existing non-empty directory into a Git working directory and push files to a remote repository

```bash
cd <localdir>
git init
git add .
git commit -m 'message'
git remote add origin <url>
git push -u origin master
```

[source](https://stackoverflow.com/a/3311824)

### Invalid path error

* Example problem in Windows: WSL creates .Zone.Identifier files. While cloning a repositry with such files, you may get the error "git clone error: invalid path 'path/filename.extension:Zone.Identifier'.  
_Solution:_ open cmd prompt as admin and run this command

```bash
git config --system core.protectNTFS false
```

[Back to Readme](README.md)
