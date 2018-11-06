# Jekyll Comments

This repository contains a commenting system for Jekyll-generated static websites.
Following instructions assume you are using the Jekyll `minima` theme. You will have
to adapt the instructions if you are using a different theme.


## Jekyll blog

Skip to next step if you have already created your Jekyll blog. To create a 
new Jekyll blog, follow the [Jekyll documentation](https://jekyllrb.com/docs/).


## Enable comments in your blog's `_config.yml`

To enable commenting, add the following to your blog's `_config.yml`:

```
...

jekyll_comments:
  show_comments: "yes"
  allow_new_comments: "yes"
  comment_server: <server-url>
  service_token: <token>
```

You will update the `comment_server` and `service_token` after deploying the server
application, which is described further below.


## Copy commenting system's templates to your blog

* If it does not already exist, create a folder `_includes` within your blog's
  root folder.

  ```
  $ mkdir _includes
  ```

* Download the following files from this repository and save them into the
  `_includes` folder:

  * `jekyll_comments.html`
  * `jekyll_comments_form.html`


## Make a local copy of theme's post.html layout

You will have to customize a layout from `minima` gem to include the commenting system's templates. You can modify a jekyll theme's functionality by copying a specific file
from theme gem and then modifying it. Jekyll uses local files of the same name
to override the theme behavior. In addition, the local folder name has to be
identical to the folder name in gem where you copied the file from.

### Create a folder in your site root directory
Since you are modifying the `post` layout, you need create a copy of the file
in your local site. You need the following steps:

In the root directory of the site, create a `_layouts` directory:

```
$ mkdir _layouts
```

### Locate minima gem's post.html on your computer
You need to determine where Ruby gems are stored on your computer.

You can figure out Ruby gem folder location by running the command
`gem environment` and looking for the value of `INSTALLATION DIRECTORY`
field. The command output should look something like:

```
$ gem environment

RubyGems Environment:
  ...

  - INSTALLATION DIRECTORY: /path/to/your/ruby/installation/lib/ruby/gems/2.3.0

  ...

```

The `minima` gem files are located within this folder:

```
$ ls -l /path/to/your/ruby/installation/lib/ruby/gems/2.3.0/gems/minima-2.5.0
```

The file you want to copy and modify is located within the `_layouts` folder:

<pre>
$ ls -l /path/to/your/ruby/installation/lib/ruby/gems/2.3.0/gems/minima-2.5.0/_layouts
default.html
home.html
page.html
<b>post.html</b>
</pre>


### Copy the gem post.html to your site
Copy `_layouts/post.html` from minima ruby gem folder into the local
`_layouts` directory just created. Go to your site's root directory
and then run the following commands:

```
$ cd _layouts
$ cp /path/to/your/ruby/installation/lib/ruby/gems/2.3.0/gems/minima-2.5.0/_layouts/post.html .
```


## Customize post.html layout to include jekyll-comments

Add the code to check and include the commenting system to your copy of `post.html`.
The code needs to be added towards the bottom of the layout, close to the `disqus`
check that `minima` theme already includes. You will add the following markup:

```
  {% if site.jekyll_comments.show_comments == "yes" %}
    {% include jekyll_comments.html %}
  {% endif %}

```

## Deploy the server application to receive comment submissions

The application is located in the repo [flask-static-comment](https://github.com/vedala/flask-static-comments). Follow instructions there to deploy the application.


## Update your `_config.yml` with server details

You will need to update your blog's `_config.yml` with two pieces of information
about comment submissions server:

* `comment_server`
* `service_token`


### Localhost deployment

If you are testing the commenting system locally, your `_config.yml` will look something
like this after the update:

```
...

jekyll_comments:
  show_comments: "yes"
  allow_new_comments: "yes"
  comment_server: http://localhost:5000
  service_token: comment-server-token-you-generated
```

### Hosted deployment

In case you deployed the comment submission server using a hosting provider, your
`_config.yml` will look something like:

```
...

jekyll_comments:
  show_comments: "yes"
  allow_new_comments: "yes"
  comment_server: https://example.com
  service_token: comment-server-token-you-generated

```


## Start the blog and submit a comment

Open/refresh your browser to see commenting system added to bottom of your blog posts.

Submit a test comment and verify you receive a success message.


## Look for pull request

Look for pull request created by the comment server in your blog repository on `github.com`.
The pull request will have the title "Comment Submission".

The pull request contains a new file which has the submitted comment data. If `awesome-blog`
is the slug of the post where comment was submitted from, the file created will look like:

```
_data/jekyll_comments/awesome-blog/a_random_filename.yml
```

The contents of the file will look like:

```
name: Joe Commenter
message: |
  This is a comment.
  This is the second line of the comment.
date: 2018-11-01 13:53:04
gravatar: d3d7ebb9768eb6f1d6cee6d0cefd341b
website: http://joes_website.com
```

## Merge pull request to include the comment into your post

The pull request serves as moderation of comments submitted on your blog. Merge the pull request if you want to accept the comment. To reject the comment, just close
the pull request.


## Submitted comment should show up

After GitHub Pages regenerates your site (or Jekyll regenerates if serving locally), the
comment should show up on your site. If serving on localhost, you will have to do a `git pull`
to pull the new comment data into your local repository.
