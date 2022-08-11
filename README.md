# Creating presentations with Reveal and Github pages

iF you are really don’t like Powerpoint.

Let’s run through how to create a presentation using both.

1. First, clone down the Reveal repo:

  `git clone https://github.com/hakimel/reveal.js.git`

2. Create a directory for the new presentation locally:

  `mkdir demopresentation`

3. Navigate to the new directory:
  
  `cd demopresentation`

4. Initialise the repo:

  `git init`

5. you can confiure git to initialise a main branch instead of master by running:
  
  `git config --global init.defaultBranch main`

6. you need to populate the repo with something before we can do anything else. So create a test file:
`new-item test.txt`

  Commit test.txt to main branch:
```
git add test.txt
git commit -m "added test.txt"
```

7. Now go to Github and create the repository that we’re going to push the local one (throw the github.com)


8. to link and push our local repository:
```
git remote add origin https://github.com/dbafromthecold/demopresentation.git
git branch -M main
git push -u origin main
```

9. Check the repo with our test file in it on Github

10. Now that the main branch has been initialised and the first commit executed we can create a gh-pages branch. The gh-pages branch, when pushed to Github, will automatically create a URL that we can use to publish our presentation. So let’s create the branch:
  
  `git branch gh-pages`
  
  Switch to the gh-pages branch:

  `git checkout gh-pages`

11. Copy the required files into the gh-pages branch from the Reveal repo:
```
copy-item ..\reveal.js\index.html
copy-item ..\reveal.js\css -recurse
copy-item ..\reveal.js\dist -recurse
copy-item ..\reveal.js\js -recurse
copy-item ..\reveal.js\plugin -recurse
```

12. Open the index.html file and replace:

  ```html
  <div class="reveal">
      <div class="slides">
          <section>Slide 1</section>
          <section>Slide 2</section>
      </div>
  </div>
  ```

  With the following:
  ```html
  <div class="reveal">
      <div class="slides">
          <section data-markdown="slides.md"
                  data-separator="^^\r?\n---\r?\n$"
                  data-separator-vertical="^\r?\n------\r?\n$"
                  data-separator-notes="^Note:"
                  data-charset="iso-8859-15"
                  data-transition="slide">
          </section>
      </div>
  </div>
  ```
  What this is doing is allowing us to use a slides.md file to create our presentation (**data-markdown="slides.md"**). Check out this [page](https://revealjs.com/markdown/) for what the other lines are doing.

13. Now create the slides.md file (just going to have a title slide initially): –

  `echo '## Demo Presentation' > slides.md`


14. Now run a commit on the gh-pages branch: –

  `git add .`

  `git commit -m "created demo presentation"`


15. And finally, add the remote location for the branch and push:

  `git push --set-upstream origin gh-pages`

16. And that’s it! Give it a few minutes and the presentation will be available at:
  
  `https://[github_login].github.io/[name_your_repository]`

## MORE:

Finally…what happens if you’re at a conference and the wifi is sketchy? No bother, if you have Python installed you can navigate to where your presentation is locally and run: –

`python -m http.server 8080`

And the presentation will be available at localhost:8080
