# Jekyll Comments

Following instructions assume you are using the Jekyll `minima` theme. You will have
to adapt the instructions if you are using a different theme.

## Jekyll blog
You can start a Jekyll blog in either public or a private repository.

## Enable  comments in your `_config.yml`

To enable commenting in your blog, add the following to your blog's `_config.yml`:

```
...

jekyll_comments:
  show_comments: "yes"
  allow_new_comments: "yes"
  comment_server: https://example.com
  service_token: <token>
```

## Copy commenting template to your blog's `_includes` folder

* If it does not already exist, create a folder `_includes` within your blog
  root folder.
* Download the following file from this repository and save them into
  `_includes` folder:
  * `jekyll_comments.html`
  * `jekyll_comments_form.html`


## Make a local copy of theme's post.html layout in preparation of customization

Copy post.html layout from the `minima` gem folder.


## Customize post.html layout to include jekyll-comments

Add the following to post.html towards the bottom of the layout close to the
`disqus` check that `minima` theme already includes:

```
  {% if site.jekyll_comments.show_comments == "yes" %}
    {% include jekyll_comments.html %}
  {% endif %}

```

## Deploy the Flask application to receive form submissions

The application is located in the repo [flask-static-comment](https://github.com/vedala/flask-static-comments)


## Start the blog and submit a comment
* Startup your blog (starting locally on your computer is fine).
* Comment submission form should show up at bottom of your posts.

## Look for pull request

Look for pull request created by the Flask comment server in your blog
repository.

An example pull request has the following file created, where `awesome-blog` is the slug of post where comment was submitted from:

`_data/jekyll_comments/awesome-blog/a_random_filename.yml`

The contents of the file look like:

```
name: Joe Commenter
message: |
  This is a comment.
  This is the second line of the comment.
date: 2018-11-01 13:53:04
gravatar: d3d7ebb9768eb6f1d6cee6d0cefd341b
website: http://joes_website.com
```

## Merge pull request to include the comment into your blog post

Creation of a pull request serves as moderation of comments submitted on your
blog. Merge the pull request if you want to accept the comment. Just close
the pull request if you want to reject the comment.

## Comment should show up

After GitHub Pages regenerates your site, the comment should show up on
your site. In case you are serving your on localhost, you will have pull the comment
data using `git pull` in your local repository.
