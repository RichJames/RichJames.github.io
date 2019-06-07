title: Running a Blog on Github with Python and virtual environments
date: June 6, 2019
author: Rich James

# How I modified the opensource.com article so I could use a virtual python environment

This blog exists because of this article:  [Run your blog on GitHub Pages with Python](https://opensource.com/article/19/5/run-your-blog-github-pages-python?utm_medium=Email&utm_campaign=weekly&sc_cid=701f20000012r6qAAA).

However, I ran into some issues when trying to follow the directions in that article.  It turns out, they were due to me wanting to create an isolated python environment, which is good practice, when following those instructions.  I created a new virtual environment in which to try the things in that article.  But, I ran into some issues coordinating between github and my environment.

So, without further ado, these are the steps I followed to successfully create this blog:

1. Create a new github repository as instructed (username/username.github.io)
2. Clone that repository onto my local machine and call it 'blog'
3. cd blog
4. mkvirtualenv -a . -p python3.6 blog
5. pip install pelican ghp-import Markdown
6. git checkout -b content
7. pelican-quickstart (and fill out as instructed)
8. git add .
9. git commit -m 'initial pelican commit to content'
10. git push origin content
11. cd content/
12. mkdir pages images
13. cp /home/rich/Pictures/me.jpg images/
14. touch first-post.md
15. touch pages/about.md
16. vim first-post.md (and add whatever text into this file)
17. vim pages/about.md (and add whatever text into this file)
18. cd ..
19. pelican content -o output -s publishconf.py
20. ghp-import -m "Generate Pelican site" --no-jekyll -b master output
21. git push origin master
22. git add content
23. git commit -m 'added a first post, a photo and an about page'
24. git push origin content

At this point, I have the blog set up with the first page and the about page, all updated at github. I can view my blog at [https://richjames.github.io/category/misc.html](https://richjames.github.io/category/misc.html).

I use virtualenvwrapper to manage python environments, which can be seen at step 4 above.  When I am done working in such an environment, just enter 'deactivate' to end the environment session.

To create more content, this is the workflow (assuming you have not started the virtual environment yet):
1. workon blog
2. cd content/
3. touch second-post.md  (example name here.)
3. vim second-post.md (add content)
5. cd ..
6. pelican content -o output -s publishconf.py
7. ghp-import -m "Generate Pelican site" --no-jekyll -b master output
8. git push origin master
9. git add content
10. git commit -m 'added a first post, a photo and an about page'
11. git push origin content
12. deactivate

Of course, the workflow here could be simplified with some scripts, but I just created all this, so that is a refinement for later. I'll provide an update later when I do that.
