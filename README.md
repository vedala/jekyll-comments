# Jekyll Comments
## Jekyll blog
You can start a Jekyll blog in either public or a private repository.

## Enable  comments in your `_config.yml`

To enable commenting in your blog, add the following to your blog's `_config.yml`:
```
jekyll_comments:
  comment_server: <url of comment server>
```

## Deploy the Flask application to receive form submissions

The application is located in the repo [flask-static-comment](https://github.com/vedala/flask-static-comments)

## Copy commenting template to your blog's `_includes` folder

* If it does not already exist, create a folder `_includes` within your blog
  root folder.
* Download the following file from this repository and save them into
  `_includes` folder:
  * jekyll_comments.html

## Startup the blog and submit a comment
* Startup your blog (stating locally on your computer is fine).
* Comment submission form should show up at bottom of your posts.

## Look for pull request

Look for pull request created by the Flask comment server in your blog
repository.

## Merge pull request to include the comment into your blog post

Creation of a pull request serves as moderation of comments submitted on your
blog. Merge the pull request if you want to accept the comment. Just close
the pull request if you want to reject the comment.

## Comment should show up

After GitHub Pages regenerates your site, the comment should show up on
your site.
