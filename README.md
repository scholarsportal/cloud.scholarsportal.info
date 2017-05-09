## cloud.scholarsportal.info

The website for the Ontario Library Research Cloud website, available at [cloud.scholarsportal.info/](https://cloud.scholarsportal.info/). This site is built with the [Hugo static site generator](https://gohugo.io/), and uses [the Agency theme](http://themes.gohugo.io/agency/).

## Using Hugo

To install Hugo on OS X using homebrew, run:

`brew update && brew install hugo` 

Run the site locally for development:

`cd mysite 
hugo server`

Then go to the URL indicated, usually [localhost:1313/](http://localhost:1313/)

Once everything is ready to go, build the site:
 
`cd mysite
hugo`

This generates your web site to the public directory, ready to be deployed to your web server.

More information on using Hugo is available at [gohugo.io](https://gohugo.io/overview/introduction/)