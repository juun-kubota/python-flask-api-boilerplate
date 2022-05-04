# python-flask-api-boilerplate

## 開発環境

- macOS Monterey 12.3.1
- Homebrew 3.4.7
- vscode 1.66.2 (Universal)
- docker desktop version 4.6.1
- pyenv 2.2.5
- Python 3.10.2 （プロジェクト適用バージョン）

## 準備

ホストPC（Mac）に以下インストールする。

### Vscode
https://code.visualstudio.com/

### Docker Desktop
https://matsuand.github.io/docs.docker.jp.onthefly/desktop/mac/install/


### pyenv
https://github.com/pyenv/pyenv

pyenvをHomebrew経由でインストールする。
Macのターミナルより以下実行。

```
$ brew update
$ brew install pyenv
$ pyenv -v
pyenv 2.2.5
```

次にPyenvの環境設定を行う。

#### For Zsh:
```
$ echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zshrc
$ echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zshrc
$ echo 'eval "$(pyenv init -)"' >> ~/.zshrc

$ echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zprofile
$ echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zprofile
$ echo 'eval "$(pyenv init -)"' >> ~/.zprofile
```

Macターミナルを再起動するか、以下コマンドで環境設定を反映する。

```
$ source ~/.zprofile
```

### Python
pyenv経由でPythonをインストールする。

```
# インストール一覧を表示
$ pyenv install --list

# Python3.10.2をインストール
$ pyenv install 3.10.2

# インストール確認
$ pyenv versions
* system (set by /Users/XXXXXX/.pyenv/version)
  3.10.2　← 追加されていること

# プロジェクトディレクトリへ移動
$ cd ~/Project_dir

# プロジェクトディレクトリ内のみにPythonのバージョンを切り替える
$ pyenv local 3.10.2　← ディレクトリ配下に「.python-version」が作成される
$ pyenv versions
  system
* 3.10.2 (set by /Users/XXXXXX/Project_dir/.python-version)
```

### Python仮想環境構築とインタープリタの設定

プロジェクトディレクトリ配下にPythonファイル（.py）を作成する。  
（ここでは「cli.py」を作成）  
<br>
プロジェクトディレクトリ配下でpython仮想環境を作成する。  
Macターミナルより以下を実行

```
$ cd ~/Project_dir
$ python -m venv .venv
```

Vscodeより、cli.pyを開くと画面下部のステータスバーにpythonのバージョンが表示されているので、クリックを行う。  
インタープリタを先ほど作成した仮想環境（.venv）に切り替える。  
今後はターミナルでの操作をVscodeのターミナルから起動、実行する。  
Vscodeの上部メニュー「ターミナル」 > 「新しいターミナル」を選択すると(.venv)の表示がされていればOK。

```
(.venv) プロジェクト名 % 
```

### Pythonモジュール

プロジェクトディレクトリ配下でpipよりVscodeで設定するPythonモジュールをインストールする。
仮想環境上でインストールする。

```
$(.venv) pip install --upgrade pip
$(.venv) pip list
Package    Version
---------- -------
pip        22.0.4
setuptools 58.1.0

$(.venv) pip install black flake8 isort mypy flask
$(.venv) pip list
Package           Version
----------------- -------
black             22.3.0
click             8.1.3
flake8            4.0.1
Flask             2.1.2
isort             5.10.1
itsdangerous      2.1.2
Jinja2            3.1.2
MarkupSafe        2.1.1
mccabe            0.6.1
mypy              0.950
mypy-extensions   0.4.3
pathspec          0.9.0
pip               22.0.4
platformdirs      2.5.2
pycodestyle       2.8.0
pyflakes          2.4.0
setuptools        58.1.0
tomli             2.0.1
typing_extensions 4.2.0
Werkzeug          2.1.2
```


### Vscodeプラグイン

- Japanese Language Pack for Visual Studio Code
- EditorConfig for VS Code
- DotENV
- Git History
- Python （Python, Pylance, Jupyter Notebook Renderers, Jupyter Keymap, Jupyter）
- autoDocstring - Python Docstring Generator

### Vscode設定

#### ① Flake8の設定

1. PythonのLint機能を有効にする。  
Python > Linting: Enabledにチェックを入れる（デフォルトはチェック済み）

2. Lint機能としてFlake8を利用するため、PyLintを無効にする  
Python > Linting: Pylint Enabledのチェックを外す

3. flake8を有効にする
Python > Linting: Flake8 Enabledにチェックを入れる

4. 1行の最大文字列数を変更する  
Python > Linting: Flake8 Argsに項目を追加する。  
--max-line-length=88」を入力して追加。

#### ② blackの設定

Python > Formatting: Providerを「black」に変更する。  
ファイル保存時の自動フォーマット機能を有効にする。  
Editor: Format On Saveにチェックする。  

#### ③ isortの設定

import文をPEP8に沿った書き方に自動的に並び替える設定。  
Editor: Code Actions On Save より setting.jsonを編集する。  

```
    "editor.codeActionsOnSave": {
        "source.organizeImports": true ← 追加
    }
```

#### ④ mypyの設定

setting.jsonに追加する。

```
"python.linting.mypyEnabled": true
```

