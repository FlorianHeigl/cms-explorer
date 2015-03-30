# Introduction #
At minimum, you must specify the URL to the "root" of the CMS and the type of CMS being tested. The "root" is the base level URL where the CMS is installed. For example, with Wordpress the root level contains the wp-content/ and wp-admin/ directories, among others.

If you specify an incorrect root level, CMS explorer will continue to run but the results will not be as expected.


# Requirements #
  * PERL 5.x
  * Getopt::Long
  * [LibWhisker2](http://www.wiretrip.net/rfp/lw.asp) (included)
  * [OSVDB API key](http://osvdb.org/api/about) (free for 100 queries per day)


# Installation #
  * Unpack archive
  * Create the file 'osvdb.key' in the cms-explorer directory, and put your OSVDB API key on the first line.
  * run ./cms-explorer.pl to ensure no errors are reported


# Option List #
|-bsproxy+|Bootstrap proxy to route findings through (fmt: host:port)|
|:--------|:---------------------------------------------------------|
|-explore|Look for files in the theme/plugin dir|
|-osvdb|Do OSVDB check for finds|
|-plugins|Look for plugins (default: on)|
|-pluginfile+|Plugin file list|
|-proxy+ |Proxy for requests (fmt: host:port)|
|-themes|Look for themes (default: on)|
|-themefile+|Theme file list (default: themes.txt)|
|-type$+|CMS type: Drupal, Wordpress, Joomla, Mambo|
|-update|Update lists from Wordpress/Drupal (over-writes text files)|
|-url$+|Full url to app's base directory|
|-verbosity+ |1-3|
|+ Option requires a value|
|$ Option is required|



# Options Explained #
  * **bsproxy** (requires value): The proxy to route any found files through. Format can be like 'http://host:port/', 'host:port' or just 'host'. If port is not specified, the default is 80.
  * **explore**: Look for additional theme/plugin files. Only supported for Drupal and Wordpress.
  * **osvdb**: Check osvdb.org for vulnerabilities in the installed components. Requires an API key be in a file called osvdb.key.
  * **plugins**: Look for plugins/module/component files. By default this is enabled and both plugins and themes will be checked.
  * **pluginfile+** (requires value): Alternative plugin file list.
  * **proxy+** (requires value): Proxy for base requests. Format can be like 'http://host:port/', 'host:port' or just 'host'. If port is not specified, the default is 80.
  * **themes** (requires value): Look for themes. By default this is enabled and both plugins and themes will be checked.
  * **themefile+** (requires value): Alternative theme file list.
  * **type+** (required, requires value): The CMS type to be tested: Drupal, Wordpress, Joomla/Mambo.
  * **update**: Update the default lists from Wordpress and Drupal. This over-writes the current files with fresh copies.
  * **url+** (required, requires value): Full URL to application's root directory (where the CMS is installed)
  * **-verbosity+** (requires value): 1-3 in increasing levels of output.


# Examples #

Test for Wordpress plugins and themes against example.com, with low verbosity and explore for additional files. Route all "found" items using the bootstrap proxy running on port 8080 of localhost.

> `perl cms-explorer.pl -url http://example.com/ -v 1 -bsproxy localhost:8080 -explore -type wordpress`

Test for Wordpress themes on example.com using themelist.txt, with full verbosity and explore using the bootstrap proxy on port 80 of localhost.

> `perl cms-explorer.pl -url http://example.com/ -v 3 -bsproxy localhost -explore -themes -themefile themelist.txt -type wordpress`

Test for Drupal plugins/themes on example.com, with normal verbosity and no exploration.

> `perl cms-explorer.pl -url http://example.com/ -type drupal`

Test for Mambo (or Joomla) components/modules and templates, and search OSVDB.

> `perl wp-explorer.pl -url http://example.com/ -type joomla -osvdb`