Translations
============

The QT GUI can be easily be translated into other languages. Here's how we
handle those translations.

Files and Folders
-----------------

### bitcoin-qt.pro

This file takes care of generating `.qm` files from `.ts` files. It is mostly
automated.

### src/qt/bitcoin.qrc

This file must be updated whenever a new translation is added. Please note that
files must end with `.qm`, not `.ts`.

    <qresource prefix="/translations">
        <file alias="en">locale/bitcoin_en.qm</file>
        ...
    </qresource>

### src/qt/locale/

This directory contains all translations. Filenames must adhere to this format:

    bitcoin_xx_YY.ts or bitcoin_xx.ts

#### Source file

`src/qt/locale/bitcoin_en.ts` is a treated in a special way. It is used as the
source for all other translations. Whenever a string in the code is change
this file must be updated to reflect those changes. Usually, this can be
accomplished by running `lupdate`

Syncing with transifex
----------------------

We are using http://transifex.net as a frontend for translating the client.

https://www.transifex.net/projects/p/bitcoin/resource/tx/

The "transifex client":http://help.transifex.net/features/client/index.html
will help with fetching new translations from transifex.


### .tx/config

    [main]
    host = https://www.transifex.net

    [bitcoin.tx]
    file_filter = src/qt/locale/bitcoin_<lang>.ts
    source_file = src/qt/locale/bitcoin_en.ts
    source_lang = en

### Fetching new translations

1. `tx pull -a`
2. update `src/qt/bitcoin.qrc`
3. `git add` new translations from `src/qt/locale/`
