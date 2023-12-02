[Back to Readme](README.md)

### Hosting on github.io
Use Github actions to automatically host the website from a Hugo theme put up as a repository.  
Follow the instructions here: https://gohugo.io/hosting-and-deployment/hosting-on-github/

If you want to test the site locally, then follow the instructions in this page: https://gohugo.io/getting-started/quick-start/

#### The old way
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

### In-line html
If you need to do things like right-aligned text, which is not availabe in native markdown, you can use html tags like this:  
`<div style="text-align: right"> your-text-here </div>`  
But hugo doesn't render html tags. So, set the unsafe parameter to true in your project’s config.toml to output HTML entered in a Markdown content file:  
```
[markup.goldmark.renderer]
unsafe= true
```
[_Source_](https://discourse.gohugo.io/t/text-alignment-not-working/36333/5)

## Hugo Coder Theme

### Changing global settings

`themes/hugo-coder/assets/scss/_base.scss` This is the file that contains the global settings for the theme.

```html
html {
  box-sizing: border-box;
  font-size: 62.5%;
}
```

REM is a relative value, based on the root font size.
Keeping the `font-size` to 62.5% will make 1rem = 10px. This is useful for setting any size in rem units.

#### Body font size

If you want the font size in body to be 16px, Under the `body` calss set it to 1.6rem. (Default is 1.8rem)

#### Page width

Under the `.container` class, change the max-width from the default `90rem`.