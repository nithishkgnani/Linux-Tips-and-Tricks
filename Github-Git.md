### Merge issues
* If the problem is "main and master are entirely different commit histories.", the following will work

      git checkout master   
      git branch main master -f    
      git checkout main  
      git push origin main -f 
[source](https://stackoverflow.com/a/66527784)

* Make an existing non-empty directory into a Git working directory and push files to a remote repository

      cd <localdir>
      git init
      git add .
      git commit -m 'message'
      git remote add origin <url>
      git push -u origin master
[source](https://stackoverflow.com/a/3311824)

