Composer Plugin Files Copier
========================================

This is a very simple Composer plugin working on the `post-install-cmd` and `post-update-cmd` events for copying from a source path to a distination folder.

I created this to avoid copying manualy the bootstrap less files into a temporary folder and overriding the variables.less for generating a custom bootstrap.css file using the less filter from the [symfony/assetic-bundle](https://github.com/symfony/assetic-bundle).


Installation / Usage
--------------------

1. In your composer.json project's file add the requirements

   ``` bash
   composer require sreichel/composer-plugin-file-copy
   ```

    ``` json
    {
        "require": {
            "sreichel/composer-plugin-file-copy": "^1.0.0"
        }
    }
    ```

2. In your composer.json project's file add the config in the extra element

   ``` bash
   composer config --json --merge extra.file-copy '[{"source": "vendor/dir", "target": "lib/vendor", "debug": true}]'
   ```

    ``` json
    {
        "extra": {
            "file-copy" : [
                {
                    "source": "vendor/dir",
                    "target": "lib/vendor",
                    "debug": true
                }
            ]
        }
    }
    ```

    or

    ``` json
    {
        "extra": {
            "file-copy" : [
                {
                    "source": "vendor/dir",
                    "target": "lib/vendor",
                    "debug": true
                }, {
                    "source": "src/Some/Bundle/less/bootstrap/*.less",
                    "target": "var/less/bootstrap"
                }, {
                    "source": "/home/username/Documents/*.{js,css}",
                    "target": "var/test"
                }
            ]
        }
    }
    ```

    >    **Note:** The destination element must be a folder. if the destination folder does not exists, it is recursively created using `mkdir($destination, 0755, true)`.

    >    **Note:** If the destination folder is not an absolute path, the relative path is calculated using the vendorDir path (`$project_path = \realpath($this->composer->getConfig()->get('vendor-dir').'/../').'/'`;)

    >    **Note:** The source element is evaluated using the php function `\glob($source, GLOB_MARK)` and a recursive copy is made for every result of this function into the destination folder


Requirements
------------

PHP 7.4 or above


Authors
-------

Abdelkadeur Seifeddine Salah - <seif.salah@gmail.com> - <http://sasedev.net><br />


License
-------

Composer is licensed under the MIT License - see the [LICENSE](./LICENSE) file for details
