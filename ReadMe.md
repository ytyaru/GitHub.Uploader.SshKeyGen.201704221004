﻿# このソフトウェアについて

GitHubアップローダで行う`ssh-keygen`, `ssh -T`コマンド操作をクラスにまとめた。

# バグ修正

* `./cui/register/SshConfigurator.py`
    * `__GetConfigTextNewHost()`
        * 結果を返してなかったので以下を追記した
            * return append.format(Host=Host, IdentityFile=IdentityFile, Port=Port)

GitHub.Upload.UserRegister.Delete.Token.SshKey.201704070801のときに初めて作成して以来、ずっとこのバグを抱えていたと思われる。今まで気づかなかった。全体的に単体テストすべき。

* `./cui/register/command/Inserter.py`。Clientを共通化したときに呼び出し側を修正し忘れていた

```python
#j_ssh = client.SshKeys.Create(token['token'], mailaddress, ssh_key_gen_params['public_key'])
j_ssh = client.SshKeys.Create(ssh_key_gen_params['public_key'], title=mailaddress)
```
`./cui/register/command/Uploader.py`も同様。
```python
#j_ssh = client.SshKeys.Create(account['MailAddress'], ssh_key_gen_params['public_key'])
j_ssh = client.SshKeys.Create(ssh_key_gen_params['public_key'], title=account['MailAddress'])
```



# 開発環境

* Linux Mint 17.3 MATE 32bit
* [Python 3.4.3](https://www.python.org/downloads/release/python-343/)
* [SQLite](https://www.sqlite.org/) 3.8.2

## WebService

* [GitHub](https://github.com/)
    * [アカウント](https://github.com/join?source=header-home)
    * [AccessToken](https://github.com/settings/tokens)
    * [Two-Factor認証](https://github.com/settings/two_factor_authentication/intro)
    * [API v3](https://developer.github.com/v3/)

# ライセンス

このソフトウェアはCC0ライセンスである。

[![CC0](http://i.creativecommons.org/p/zero/1.0/88x31.png "CC0")](http://creativecommons.org/publicdomain/zero/1.0/deed.ja)

Library|License|Copyright
-------|-------|---------
[requests](http://requests-docs-ja.readthedocs.io/en/latest/)|[Apache-2.0](https://opensource.org/licenses/Apache-2.0)|[Copyright 2012 Kenneth Reitz](http://requests-docs-ja.readthedocs.io/en/latest/user/intro/#requests)
[dataset](https://dataset.readthedocs.io/en/latest/)|[MIT](https://opensource.org/licenses/MIT)|[Copyright (c) 2013, Open Knowledge Foundation, Friedrich Lindenberg, Gregor Aisch](https://github.com/pudo/dataset/blob/master/LICENSE.txt)
[bs4](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)|[MIT](https://opensource.org/licenses/MIT)|[Copyright © 1996-2011 Leonard Richardson](https://pypi.python.org/pypi/beautifulsoup4),[参考](http://tdoc.info/beautifulsoup/)
[pytz](https://github.com/newvem/pytz)|[MIT](https://opensource.org/licenses/MIT)|[Copyright (c) 2003-2005 Stuart Bishop <stuart@stuartbishop.net>](https://github.com/newvem/pytz/blob/master/LICENSE.txt)
[furl](https://github.com/gruns/furl)|[Unlicense](http://unlicense.org/)|[gruns/furl](https://github.com/gruns/furl/blob/master/LICENSE.md)
[PyYAML](https://github.com/yaml/pyyaml)|[MIT](https://opensource.org/licenses/MIT)|[Copyright (c) 2006 Kirill Simonov](https://github.com/yaml/pyyaml/blob/master/LICENSE)

