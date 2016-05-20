---
layout: post
title: Contributing to the blog
author: Daniel
---

Contributing to this blog is easy. To do it, make sure you have a fork of the [the main repository](https://www.github.com/wowico/wwc) on GitHub. Then, from the *Shell Terminal*:

```shell
# enter the repo
cd wwc
# make sure your fork is up to date:
git pull
```

Now, you might like to copy the template file:

```shell
cp _posts/2016-05-16-template.md _posts/2016-05-20-<pick-a-title>.md
```

Once you've done that, you need to edit the newly created blog entry. In the cloud, the best way to do this is to open up the *Jupyter Notebook* interface, navigate to `wwc/_posts`, and open it up for editing.

Once you've edited it, save it, and return to the *Shell Terminal*. Then:

```shell
git status
git add _posts/2016-05-20-<pick-a-title>.md
# if you're having authentication errors,
# check out our page on 'adding your bio'
git commit "Adding a blog post"
git push origin gh-pages
```

If you go to your fork, which should be at `https://www.github.com/<username>/wwc`, you should now see your new files. You can then submit a pull request to the main repository. We'll approve it, and your post will appear here!


Good luck!
