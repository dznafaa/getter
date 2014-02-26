# Getter

Getter is a secure, single-file, PHP-powered download handler and logging script. Getter gives your clients the ability to download files without revealing the actual name or directory structure of your server. Built-in hotlink protection also prevents bandwidth leeching from other websites.

## Installation and Configuration

[Download the latest version][a1] of Getter, and copy `download.php` to the directory where you normally serve your downloads.

All editable options are contained in the Configuration class:

 - `BASE_DIRECTORY` - Set the directory that all downloadable files will be stored in
 - `HOTLINK_PROTECTION` - Flag to set hotlink protection
 - `HOTLINK_PROTECTION_ALLOW_NULL`
 - `HOTLINK_REDIRECT_URL` - The redirect destination when hotlinking is detected
 - `LOG_DOWNLOADS` - Flag to set logging
 - `LOG_FILENAME` - The filename of the download log
 - `PANEL_ON` - Flag to turn the Web Panel on
 - `PANEL_TOKEN` - The URI token used to reach the Web Panel.
 - `PANEL_ITEMS_MAX_NUM` - Maximum number of recent log entries listed on the Web Panel
 - `PANEL_USERNAME` - HTTP Auth username for the Web Panel
 - `PANEL_PASSWORD` - HTTP Auth password for the Web Panel
 - `PANEL_CSS` - Internal CSS stylesheet for the Web Panel
 - `$MIME_TYPES`
 - `$HOTLINK_WHITELIST`

## Serving Downloads
There are 3 ways to download a file using Getter:

```html
download.php?[FILENAME]
download.php?[FILENAME]/[ALIAS]
download.php?[FILENAME_HASH]/[ALIAS]
```
Given a filename, Getter will perform a [depth-first search][b1] through the directory set in `BASE_DIRECTORY`. The `[FILENAME]` should be unique for all files stored in the base directory, even if those two files are not in the same folder/sub-folder. When two files share the same name, Getter will transfer the first file of that name it encounters, which may not be the desired result.

When `[ALIAS]` is provided, the user will be prompted to save the fileunder the alias name, instead of the actual filename.

The `[FILENAME_HASH]` is an [MD5 hash][b2] of the `[FILENAME]` you wish to download. This prevents the use from knowing the actual name of the file you are serving. When using filename hashes, you must provide an alias.

### Hotlink Protection
Redirect to a page or serve 403 Forbidden error.

## Managing the Log
When `LOG_DOWNLOADS` is enabled, Getter will log every download that it handles on the server into a single CSV. This file is generated in the same directory that Getter resides in. It will collect a date-timestamp, the client's IP Address, the Request URL, and the file that was requested.

### Acessing the Web Panel
When `PANEL_ON` is set to __true__, you can manage the log using Getter's built-in web panel. Use the `PANEL_TOKEN` token as part of the URL to access this. The default token is __admin__, and the default URL is:

```html
http://www.yourdomain.com/download.php?admin
```

NOTE: Clearing the log deletes the logged data off the server, not just the page. You cannot recover your log data after you've cleared it.

### Using CSV
The logs generated by Getter are plain text ASCII CSV files. These logs can be viewed raw by any ASCII editor or Word Processor like Notepad, Wordpad, and Microsoft Word. The file should can easily be imported into spreadsheet applications like Excel.

## Copyright and License

Copyright &copy; 2007-2014 Gowon Patterson, Gowon Designs.

This program is distributed under the terms of the [GNU General Public License Version 2][license].

[a1]: https://github.com/gowondesigns/getter/zipball/master
[b1]: http://en.wikipedia.org/wiki/Depth-first_search
[b2]: http://en.wikipedia.org/wiki/MD5
[license]: http://www.gnu.org/licenses/gpl-2.0.html
