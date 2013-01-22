---
layout: post
title: Wordpress &rarr; Jekyll, Disqus, and S3 
tags:
status: draft
type: post
published: true
meta: {}
---
This is a (relatively) complete guide to converting a Wordpress blog over to
[Jekyll](http://jekyllrb.com/), using [Amazon's S3](http://aws.amazon.com/s3/) to host the content, and [Disqus](http://disqus.com/) to host comment threads.

To serve as a reference, you can find the configuration and content for this website on GitHub at [https://github.com/peat/pdo](https://github.com/peat/pdo).

Please consider three big caveats before proceeding:

- This process takes about a day for an experienced web developer with a moderate
amount of content. Expect to gnaw on healthy chunk of Ruby, Yaml, Markdown, HTML and CSS.
- This isn't a full tutorial on how to configure and run Jekyll. I highly recommend
[R-ing TFM](https://github.com/mojombo/jekyll/blob/master/README.textile) before
diving in.
- This guide does not include converting your Wordpress theme; this is strictly about moving
content from a Wordpress blog to Jekyll + Disqus on S3.

This information is current as of January, 2013. If you find mistakes, or have
suggestions, please let me know in the comments below!

Without further ado ...

### The Game Plan

1. [Introducing](#introduction) ...
2. [Install Jekyll and its dependencies](#installing-jekyll).
3. [Archive posts, comments, and pages from Wordpress](#archive-wp).
4. [Convert the Wordpress archive into Jekyll posts](#import-posts).
5. [Import the Wordpress comments into Disqus](#import-comments).
6. [Configure Jekyll](#configure-jekyll).
7. [Create your basic layouts](#create-layouts).
8. [Insert your Disqus threads into your Jekyll posts](#map-disqus).
9. [Generate Atom feed for blog posts](#create-atom).
10. [Generate sitemap.xml and robots.txt for search engines](#create-search).
11. [Configure Amazon S3 and Route 53 for hosting](#setup-aws).
12. [Upload your site](#upload-site).
13. [Party on](#party)!

<a id="introduction"> </a>
### 1. Introducing ...

There are many players in this particular drama, each responsible for a separate role in getting your site converted.

- [_Jekyll_](https://github.com/mojombo/jekyll) is the tool that generates static HTML pages from your content.
- [_Disqus_](https://disqus.com/) is a service that hosts discussion threads that you can embed in your static pages.
- [_S3_](http://aws.amazon.com/s3/) is a scalable, cheap, web accessible data store. That's where your website will live.
- [_Route 53_](http://aws.amazon.com/route53/) is a scalable, cheap DNS hosting service .. that you _may_ be required to use.

Now that we're acquainted, lets get started ...

<a id="installing-jekyll"> </a>
### 2. Install Jekyll

To install Jekyll and it's dependencies:

- Ensure you have a Ruby interpreter and `gem` on your computer. If you don't, you can find installation instructions [here](http://www.ruby-lang.org/en/downloads/).
- Run `gem install jekyll`, and if you have problems, check out the [official installation instructions](https://github.com/mojombo/jekyll/wiki/install).

<a id="archive-wp"> </a>
### 3. Archive Wordpress Content

- Login to your Wordpress administration site.
- Click _Tools_ &rarr; _Export_ &rarr; _All Content_ &rarr; _Download Export File_

Your browser will download an archive of all _written_ content from your blog -- that is, pages, comments, blog posts, etc.

You still need to grab all of the images and other assets hosted on your site, by downloading the contents of your `wp-content/uploads` folder.

<a id="import-posts"> </a>
### 4. Convert Posts

Thankfully, some very smart and good looking people have provided a very convenient script for converting your Wordpress archive into Jekyll documents:

- Create the directory that you want to store all of your Jekyll content in.
- Run this from the command line:

{% highlight bash %}
$ ruby -rubygems -e 'require "jekyll/migrators/wordpressdotcom"; Jekyll::WordpressDotCom.process("wordpress.xml")'
{% endhighlight %}

If you run into trouble, check out the [official documentation](https://github.com/mojombo/jekyll/wiki/blog-migrations).

This will create a rudimentary Jekyll site, with all of your content located in the `_posts` folder.

<a id="import-comments"> </a>
### 5. Import Disqus Comments

To import all of your Wordpress comment threads into Disqus:

- Go to the [Disqus website](http://disqus.com/) and click the _"Get this on your site"_ button. You will be led through the process of creating an account (if you don't already have one), and setting up a new site profile.
- Go to your [Disqus dashboard](http://disqus.com/dashboard), select the site you've created, then _Tools_ &rarr; _Import_ &rarr; _Wordpress_
- Upload your Wordpress archive file directly. _Do NOT install or use the Wordpress plugin to migrate your comments._

This will kick off the import process. It can take anywhere from a couple of minutes to several hours, so lets go work on some other stuff in the meantime.

<a id="configure-jekyll"> </a>
### 6. Configure Jekyll

Jekyll has a very rational configuration set by default, but we need to change one parameter to ensure that your permalinks will stay consistent, and that Disqus will map your comments to the correct URLs.

Create a `_config.yml` file if you don't already have one, and add the line:

{% highlight yaml %}
permalink: /:year/:month/:day/:title/
{% endhighlight %}

<a id="create-layouts"> </a>
### 7. Create Layouts

This is the part where I must point you at the [Jekyll documentation](https://github.com/mojombo/jekyll) to learn about their templating system. 

If you're curious about how this site (peat.org) works, check out the [GitHub repository](https://github.com/peat/pdo), particularly the [\_layouts](https://github.com/peat/pdo/tree/master/_layouts) folder. Everything you see here is in that repository. Have fun!

While you're hacking on your layouts, I highly recommend running `jekyll --auto --server`, so that you can interactively tweak your templates. For more information about running Jekyll, check out [the docs](https://github.com/mojombo/jekyll/wiki/usage).

<a id="map-disqus"> </a>
### 8. Insert Disqus Threads

To add Disqus comment threads into your post template:

- Go to your [Disqus dashboard](http://disqus.com/dashboard), select the site you've created, then _Settings_ &rarr; _Install_ &rarr; _Universal Code_
- Copy the provided Javascript into your `_layouts/post.html` template.
- Update the `disqus_url` variable to point at the permalink for the post.
- Update the `disqus_title` variable to properly escape the name of the post.

Take a look at [the peat.org post template](https://github.com/peat/pdo/blob/master/_layouts/post.html) to see an example.

<a id="create-atom"> </a>
### 9. Create an atom.xml Feed

If you would like your blog posts to be picked up by a feed reader (like [Google Reader](http://reader.google.com)):

- Add the following tag to the `<head>` of your `_layouts/default.html` file:

{% highlight html %}
<link rel="alternate" type="application/atom+xml" title="some title" href="/atom.xml" />
{% endhighlight %}

- Copy my [template atom.xml feed](https://github.com/peat/pdo/blob/master/atom.xml) into the root folder for the site, and change out the names and URLs to fit your site.

<a id="create-search"> </a>
### 10. Create sitemap.xml and robots.txt

Search engines love metadata, and using `sitemap.xml` and `robots.txt` to manage their crawling behavior is a good idea.

To create the `sitemap.xml` file, use Michael Levin's [sitemap Jekyll plugin](http://www.kinnetica.com/projects/jekyll-sitemap-generator/). Follow the provided instructions to install and configure the plugin. It will run automatically when you regenerate the site, so that's that.

For the `robots.txt` file, simply create the `robots.txt` file in your site's root directory. I have a simple one in the [peat.org repo](https://github.com/peat/pdo/blob/master/robots.txt), or you can build your own using this [handy generator](http://www.mcanerin.com/EN/search-engine/robots-txt.asp).

<a id="setup-aws"> </a>
### 11. Set up Amazon S3 and Route 53.

If you don't have an Amazon Web Services account, [sign up for one](https://portal.aws.amazon.com/gp/aws/developer/registration/index.html).

As a quick introduction, S3 is an extremely scalable, cheap, and reliable method of hosting data on the web. This makes it ideally suited for statically generated blogs. Route 53 is an extremely scalable, cheap, and reliable DNS hosting system. Please note that Route 53 is _required_ if you plan on hosting your Jekyll site at your domain apex (eg: http://peat.org/ instead of http://subdomain.peat.org/).

Amazon is rather picky about how this is done, so unfortunately I must refer you to their documentation for [step by step instructions](http://docs.aws.amazon.com/AmazonS3/latest/dev/website-hosting-custom-domain-walkthrough.html).

Good luck!

<a id="upload-site"> </a>
### 12. Upload Your Site (Almost There ...)

As you work on your site, you'll frequently re-upload the entire site, nuke it, and tweak individual files.

In order to make this simpler, I've created a [Rakefile](https://github.com/peat/pdo/blob/master/Rakefile) which:

- Understands different site locations and credentials (eg: test, staging, production).
- Sets accurate Content-Type headers for the content on S3.
- Uploads files in parallel to speed things up.
- Nukes an entire site from S3 if (when) things get messy.

To use it, you need to create a configuration file containing your AWS credentials and bucket information on a per-environment basis.

The configuration file is named `.upload.cfg.yml` and resides in the root directory of your Jekyll site. Here's an example of what it contains:

{% highlight yaml %}
test:
  aws_access_key_id: YOUR_ACCESS_KEY_ID
  aws_secret_access_key: YOUR_SECRET_ACCESS_KEY
  s3_bucket: YOUR_S3_BUCKET_NAME
  
production:
  aws_access_key_id: YOUR_ACCESS_KEY_ID
  aws_secret_access_key: YOUR_SECRET_ACCESS_KEY
  s3_bucket: YOUR_S3_BUCKET_NAME
{% endhighlight %}

... where `test` and `production` are the site names you can reference when using the Rakefile.

To build and upload your entire site, simply:

{% highlight bash %}
$ rake SITE=site_name
{% endhighlight %}

To upload a single file:

{% highlight bash %}
$ rake upload SITE=site_name FROM=local_path TO=remote_path
{% endhighlight %}

To delete a remote site, with confirmation:

{% highlight bash %}
$ rake napalm SITE=site_name
{% endhighlight %}

For more information, just run `rake -T`.

<a id="party"> </a>
### 13. Party!

Congratulations! If all goes well, you can point your favorite web browser at your new website.

Now it's time to crack open a frosty beverage, pat yourself on the back. You deserve it.
