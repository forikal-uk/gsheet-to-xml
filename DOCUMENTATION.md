# Installation
- Clone this project
- Run `composer install`
- test the console app: `php bin/gsheet-to-xml.php --help`

__Note__ Make sure you're using at least PHP 7.1

# Google API Setup

See: [How to: Google API Setup](https://github.com/xmlsquad/xml-authoring-library/blob/master/HowTo-GoogleAPISetup.md)


# Usage
`php bin/gsheet-to-xml.php {URL} [--credentials=client_secret.json] [--recursive]`

`{URL}` should be either Drive or Sheets URL in one of following formats
- https://drive.google.com/drive/folders/xxxxxxxxxx-xxxxxxxxx-xxxxxxxxxxxx
- https://docs.google.com/spreadsheets/d/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx/edit

`-c, --credentials` is optional parameter that specifies path to the credentials file with Google secret. Path
must be relative to the directory you're calling the script from.

`-r, --recursive` if the Google Drive entity is a Google Drive folder, this option specifies whether or not to recurse 
through sub-directories to find sheets.

# Behavior

- Empty rows are skipped without notice.
- Files ending with _ (underscore) are ignored (e.g. foo_.xslx, foo_)
- Tabs ending with _ (underscore) are ignored
- When parsing folders, for every spreadsheet found new `<Product><Inventory>` XML element is created with `src-sheet-url` attribute
containing the spreadsheet ID.

# Tests

If the package is being edited in standalone context:
Run `./vendor/bin/phpunit` to execute test suite

If [the package is being edited in context of some other parent project](https://github.com/xmlsquad/gsheet-to-xml/issues/21#issuecomment-400342043) you could run phpunit from the root directory and point to this package's tests folder explicitly:
```bash
$ pwd
/some/parent/project/root/folder
$ ./vendor/phpunit/phpunit/phpunit vendor/xmlsquad/gsheet-to-xml/tests/
```


# Resources
- https://www.fillup.io/post/read-and-write-google-sheets-from-php/
- https://developers.google.com/sheets/api/samples/reading
- https://stackoverflow.com/a/16840612
- https://developers.google.com/sheets/api/guides/concepts

# Troubleshooting
- You have to enable both Sheets and Drive API
- You have to share files/folders with email in credentials JSON file

