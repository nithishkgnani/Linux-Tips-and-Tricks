[Back to Readme](README.md)

### Hosting on github.io
Once your website made using Hugo, is ready and you have tested in local host, to host it on GitHub pages:
1. Create an empty repository named _<USERNAME>.github.io_
2. `cd <mysite> #(note: here should be 'cd' + the full path to <mysite>)`  # here <mysite> is your website name created using Hugo
3. `hugo` # this builds your website files into the public folder
4. Go to the directory of the public folder and push the files into the repository you created:  

        cd public  
        git init  
        git add .
        git remote add origin https://github.com/USERNAME/USERNAME.github.io.git  
        git commit -m “commit message”  
        git push origin master  
    Note: if you face brange merge issues, you might want to [check this out](https://github.com/nithishkgnani/Linux-Tips-and-Tricks/wiki/github-git#merge-issues).
5. Your website should be up and running in a few moments.

[_Source_](https://levelup.gitconnected.com/build-a-personal-website-with-github-pages-and-hugo-6c68592204c7)

[Back to Readme](README.md)