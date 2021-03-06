# Trakt.tv import/export tools

## Purpose

 * Import Movies or TVShows IDs from CSV file format into Trakt.tv.

 * Export Movies or TVShows IDs from Trakt.tv list into CSV file format.

 * Create trakt.tv custom list from TDMB discover with filter.

## Requirements

You must use Python 2.7.x.

##### On Ubuntu/Debian Linux system

Ensure you are running Python 2.7
```
        $ python -V
Python 2.7.9
```

Install need module dependencies

        $ apt-get install python-dateutil python-simplejson python-requests python-openssl jq

##### On Windows system

 Download the installer: https://www.python.org/ftp/python/2.7.16/python-2.7.16.msi

 Ensure you are running Python 2.7
```
        C:\Python27>python.exe -V
Python 2.7.16
```

 Install need module dependencies

        C:\Python2.7\Scripts\easy_install-2.7.exe simplejson requests

## Usage

* Create an [Trakt.tv application](https://trakt.tv/oauth/applications) to have your own ``client_id`` and ``client_secret``, https://trakt.tv/oauth/applications.
You only need to fill up the ``Name`` with a ``Description`` and ``Redirect uri`` to whatever (i.e. https://zapp.com, it is not being used), leave the rest empty and click on ``SAVE APP``.

* Run the script to create a default config file ``config.ini``

        $ python export_trakt.py

* Edit the config file ``config.ini`` and specify the ``client_id`` and ``client_secret`` as well as any other settings appropriate to your enviromenent, eg: URL, proxy, etc...
Refer to ``Configuration details`` section for more information.

        $ vim config.ini

* Run the script to authenticate against Trakt.tv API using the PIN method and it will generate you an ``oauth_token``.
You will be prompted to open a link into a browser and paste the pincode back to the script. 
Make sure you save the generated ``oauth_token`` into the config file ``config.ini`` for later use.

        $ python export_trakt.py

## Configuration

#### Configuration sample
```text
[TRAKT]
client_id = xxxxxxxxxxxxxxxxxxxxxxxxx
client_secret = xxxxxxxxxxxxxxxxxxxxxx
oauth_token = xxxxxxxxxxxxxxxxxxxxxxx
baseurl = https://api-v2launch.trakt.tv
[SETTINGS]
proxy = False
proxy_host = https://127.0.0.1
proxy_port = 3128
```

#### Configuration details

 * ``client_id``: Uniq ID to identify your application, https://trakt.tv/oauth/applications
 * ``client_secret``: Uniq ID to identify your application, https://trakt.tv/oauth/applications
 * ``oauth_token``: Uniq ID to identify yourself against your application
 * ``baseurl``: API base URL, depends on the platfrom, eg: Production (https://api-v2launch.trakt.tv) or Staging (https://api-staging.trakt.tv)
 * ``proxy``: True/False setting to enable proxy support
 * ``proxy_host``: Full URI of the proxy
 * ``proxy_port``: Port of the proxy to connect to

## Developer documentation

        $ pydoc `pwd`/import_trakt.py

        $ pydoc `pwd`/export_trakt.py

## Usage 
### Export usage
```text
usage: export_trakt.py [-h] [-v] [-c CONFIG] [-o [OUTPUT]]
                       [-t {movies,shows,episodes}]
                       [-l {watchlist,collection,history}] [-u USERLIST] [-C]
                       [-D] [-V]

This program export Movies or TVShows IDs from Trakt.tv list.

optional arguments:
  -h, --help            show this help message and exit
  -v, --version         show program's version number and exit
  -c CONFIG, --config CONFIG
                        allow to overwrite default config filename, default
                        config.ini
  -o [OUTPUT], --output [OUTPUT]
                        allow to overwrite default output filename, default
                        None
  -t {movies,shows,episodes}, --type {movies,shows,episodes}
                        allow to overwrite type, default movies
  -l {watchlist,collection,history}, --list {watchlist,collection,history}
                        allow to overwrite default list, default history
  -u USERLIST, --userlist USERLIST
                        allow to export a user custom list, default None
  -C, --clean           empty list after export, default False
  -D, --duplicate       remove duplicate from list after export, default False
  -V, --verbose         print additional verbose information, default True

Read a list from Trakt API. Export them into a CSV file.
```

## Examples
### Sample export usage

Export all movies from wathclist:

        $ ./export_trakt.py -c config.ini -t movies -o export_movies_wathclist.csv -l watchlist

Export all tvshows from the history list:

        $ ./export_trakt.py -c config.ini -t shows -o export_shows_history.csv -l history

Export all episodes from the history list:

        $ ./export_trakt.py -c config.ini -t episodes -o export_episodes_history.csv -l history

Export all shows from the history list and remove duplicate:

	$ ./export_trakt.py -c config.ini -t shows -o export_shows_history.csv -l history -D

Export all movies from a user list:

	$ ./export_trakt.py -c config.ini -t movies -u <username> -o export_movies_<username>.csv

## Support

To get support, please create new [issue](https://github.com/xbgmsharp/trakt/issues)

## Licence

This script is free software:  you can redistribute it and/or  modify  it under  the  terms  of the  GNU  General  Public License  as published by the Free Software Foundation.

This program is distributed in the hope  that it will be  useful, but WITHOUT ANY WARRANTY; without even the  implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License for more details.

See <http://www.gnu.org/licenses/gpl.html>.
