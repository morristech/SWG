SWG - Static Website Generator
==============================

Copyleft by Simone Margaritelli <evilsocket@gmail.com>

What is SWG ?
-------------

SWG is a new generation static website generator, featured by the Mako (http://www.makotemplates.org/) template system, born from the need to
have both performances and "WEB 2.0" contents and capabilities.

Given a set of files, one for each page/article, one for each author and one for the categories hyerarchy, SWG will read the configuration file
you specify from command line and generate a complete static website, with tags and categories indexing.

Installation
------------

To get the latest released version:

::

    pip install swg

Create a new website
--------------------

To start a new website, type:

::

    swg --create website-folder-name

An example site with a basic structure will be created inside the 'website-folder-name' directory.
Then you can type:

::

    cd website-folder-name
    swg --serve

To test the website locally.
The first article is about customization and basic configuration, so read it carefully.

Generate your website
---------------------

Once you are in the directory containing your website definition (with a swg.cfg file in it), just run:

::

    swg --generate

To start website generation, other options are available, use

::

    swg --help

To a display the complete list.

Importing from another platform
-------------------------------

Right now, there's the swg-wordpress script you can use to convert a WordPress XML backup file to the
SWG format, to use it consider the following:

::

    swg-wordpress --help
    - SWG Wordpress Backup Importer -
    
    Usage: swg-wordpress -i wordpress-backup.xml -u 'http://www.your-site-url.com' <options>
    
    
    Options:
      -h, --help            show this help message and exit
      -i WPBACKUP, --input=WPBACKUP
                            The Wordpress XML backup file.
      -u SITEURL, --url=SITEURL
                            URL of the destination website.
      -o OUTDIR, --output=OUTDIR
                            Output directory, default is the current working
                            directory.
      -e FILEEXT, --extension=FILEEXT
                            Output file extension, default is txt.
      -I IMGDIR, --images=IMGDIR
                            If specified, it's the path where the importer will
                            try to download images referenced by articles.

So let's say for instance, that you have your wp.xml file and you want to export it to the 'example-site.com' directory, downloading
images referenced by the articles into the 'example-site.com/images' directory (the import will replace properly image urls), you
will use the command line:

::

    swg-wordpress -i wp.xml -u http://www.example-site.com -o 'example-site.com' -I 'example-site.com/images'

And it's all done!
Now you just have to create the templates, fix the categories hyerarchy inside the file 'example-site.com/db/categories.txt', customize
your own description inside 'example-site.com/db/your-nickname.txt' and make the configuration file following the example below.

An example configuration file
-----------------------------

::

    # DB files extension
    dbitem_ext = txt
    # URL of the site you are going to generate
    siteurl    = http://www.example-site.com
    # Site name / description
    sitename   = An example site generated by SWG
    # Site charset
    charset    = utf-8
    # Site language
    language   = it
    # Comma separated site keywords
    keywords   = some, html, keywords, here
    # Site destination basepath
    basepath   = 
    # Site page files output extension
    page_ext   = html
    # Generated site output path
    outputpath = out
    # Items (dirs or files) to copy from datapath to outputpath (eg. static files, css, etc)
    copypaths  = css, images, .htaccess
    # Command to execute once the generation is finished, for instance an rsync :)
    transfer   = rsync -ravz out/* -e ssh user@example-site.com:/var/www/example-site.com/htdocs/
    # Enable or disable the pager on categories, index, tags and author pages
    pager      = true
    # If pager is enabled, this is the maximum number of items per page
    items_per_page = 10
    # Compress pages (ie. index.html.gz) and create (or update) .htaccess file to serve them as html files
    gzip       = true
    # Compression level, 0 to 9
    compression = 9
    # Clean output html with TIDY
    tidyfy = true

Pretty self explanatory isn't it ? :)

Testing your website locally
----------------------------

From version 1.2.4, SWG offers the possibility to test your website locally, once you are in the directory containing your website definition 
(with a swg.cfg file in it), run the following command:

::

    swg --serve

This will start the website generation and a test webserver on http://localhost:8080/ .

Example project
---------------

For an example site, look at my personal blog github repo located here https://github.com/evilsocket/evilsocket.net

Enjoy ^^
