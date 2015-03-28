finishGoogleCodeGitHubWikiMigration
===================================
by Morgan Aldridge <morgant@makkintosshu.com>

OVERVIEW
--------

As you probably now know, Google is [shutting down Google Code in less than a year](http://google-opensource.blogspot.com/2015/03/farewell-to-google-code.html) and is encouraging users to switch to other open source hosting platforms such as [GitHub](https://github.com). They have a handy [Export to GitHub](https://code.google.com/export-to-github/) tool, which is easy, if a bit slow.

It appears to do a good job on the source code repository side of things, but has a few issues for project wikis (despite automatically converting to Markdown):

1. It doesn't preserve history or images.
2. It exports the wiki data into [a separate 'wiki' branch](https://code.google.com/p/support-tools/wiki/GitHubExporterFAQ#Where_did_my_Google_Code_wikis_go), not the GitHub project wiki.

There's nothing I can do about the former, but I was able to easily automate resolution of the latter since [GitHub allows you to clone project wikis to local repositories](https://help.github.com/articles/adding-and-editing-wiki-pages-locally/). Enter `finishGoogleCodeGitHubWikiMigration`, which--given a Google Code project exported to GitHub--takes the `ProjectHome.md` wiki page and makes it into the project's `README.md` file, plus moves all the wiki pages over to the GitHub project's wiki. It also fixes the page links in the docs.

USAGE
-----

1. You must create at least one page in your GitHub project's wiki (I just created the default `Home` page).
2. Change to a directory where you _do not_ already have the GitHub project in question checked out (for safety reasons, it wants to work on a fresh copy and will not proceed if you already have a copy).
2. Run `finishGoogleCodeGitHubWikiMigration git@github.com:<username>/<projectname>.git` to be cloned from GitHub.
3. It should clone the repositories & do its work, leaving you with two locally-modified repositories `<project>` & `<project>.wiki`, having committed its changes to each.
4. You should then go into each repository & review all the changes. I suggest at least a `git log` & `git diff HEAD^1` on each.
5. If, **and only if**, you feel the changes are correct, you can perform a `git push` on each to commit the changes back to the repository on GitHub.
6. Lastly, you can delete the `wiki` branch and the `<project>` & `<project>.wiki` local repositories, if you like.

**NOTE**: This tool modifies the repositories, if you don't like the changes it makes, **DO NOT** push the changes back to GitHub!

You can also [set the "project moved" flag on the Google Code project](https://code.google.com/p/support-tools/wiki/GitHubExporterFAQ#Setting_the_"Project_Moved"_Flag) if you want it to permanently redirect to the GitHub project, but I've found you cannot revert the change.

LICENSE
-------

Copyright (c) 2015 Morgan T. Aldridge

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
