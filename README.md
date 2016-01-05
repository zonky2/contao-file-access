Contao File Access
=====================

Contao extension that allows file access restrictions for frontend users.

## Usage

After installing this extension, you will have the ability to activate the file protection in the file manager of the backend. Simply edit a file or folder and enable the protection. You also need to select one or more member groups for which the file or folder should be accessible. If you select none, the file will not be accessible in general (but can still be accessed via the download content element for example).

To enable the file access restriction, you need to redirect all URLs accessing the files to the `file.php` script, e.g. by using the following RewriteRule in your `.htaccess`:

```
RewriteRule ^(files/.*)$ file.php?file=$1 [L]
```

The extension comes with an example file called `.htaccess.fileaccess` which you can enable (and change according to your needs).

It is recommended to only redirect file URLs for files that are in fact protected. To achieve this, you can create a new subfolder, e.g. `files/protected` and change the RewriteRule to

```
RewriteRule ^(files/protected/.*)$ file.php?file=$1 [L]
```

This way all public files can be accessed directly and will not cause additional server load by processing and sending it via PHP.

## Important Note

Since this access restriction is done via PHP, the file is also sent to the client via PHP. This means that the `max_execution_time` needs to be sufficiently large, so that any file can be transferred to the client before the script is terminated. Thus you should be aware that problems can occur if a file is either very large or the client's connection to the server is very slow, or both.
