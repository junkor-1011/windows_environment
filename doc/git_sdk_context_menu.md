Git SDKをContext Menuへ追加
===========================

## 動機

- [Git for Windows SDK](https://github.com/git-for-windows/build-extra/releases)を先にインストール済みの(普通の)Git for Windows
  と競合しないようにインストールし、コンテクストメニュー（右クリック表示）に加えたいと思ったため、そのメモや参考リンク集

## 作業概要

### Step1. コンテクストメニュー追加（右クリックで任意のフォルダ上で開ける）

（方針）`reg`ファイルを作成し、管理者権限で実行してレジストリに登録

- `Git for Windows SDK`のインストール場所は`C:\Applications\git-sdk-64`にしたので、状況に応じて適宜読み替え
- ディレクトリで開ければ良いので、そのような感じで設定
- 以下のような内容の`git_sdk_context_menu.reg`(名前は適当)を作成して任意の場所で実行
    - [実際に使ったもの](./execute/git_sdk_context_menu.reg)

```
Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\Directory\Shell\git_sdk_Shell]
@="Open Git Bash(SDK)"
"Icon"="C:\\Applications\\git-sdk-64\\git-bash.exe"

[HKEY_CLASSES_ROOT\Directory\Shell\git_sdk_Shell\command]
@="\"C:\\Applications\\git-sdk-64\\git-bash.exe\" \"--cd=%v.\""

[HKEY_CLASSES_ROOT\Directory\Background\Shell\git_sdk_Shell]
@="Open Git Bash(SDK)"
"Icon"="C:\\Applications\\git-sdk-64\\git-bash.exe"

[HKEY_CLASSES_ROOT\Directory\Background\Shell\git_sdk_Shell\command]
@="\"C:\\Applications\\git-sdk-64\\git-bash.exe\" \"--cd=%v.\""
```

あまり詳しくないが、おそらく`git_sdk_Shell`のところは任意。
元々インストーラで入れている普通の`Git for Windows`と競合するとまずいはずなので、重複しなさそうな名前をつけておく。

  
### Step2. タスクバーにピン止め

- 基本はショートカットをタスクバーに貼り付けるだけ
- ホームディレクトリで開くようにしたかったので、`workspace`を編集
- [ここ](https://www.granfairs.com/blog/staff/gitbash-setting-shortcut)を参考

------

## 参考リンク

#### Regファイル作成時

- https://www.it-swarm.dev/ja/git/%E3%80%8C%E3%81%93%E3%81%93%E3%81%A7gitbash%E3%82%92%E9%96%8B%E3%81%8F%E3%80%8D%E3%82%B3%E3%83%B3%E3%83%86%E3%82%AD%E3%82%B9%E3%83%88%E3%83%A1%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%92windows%E3%82%A8%E3%82%AF%E3%82%B9%E3%83%97%E3%83%AD%E3%83%BC%E3%83%A9%E3%83%BC%E3%81%AB%E8%BF%BD%E5%8A%A0%E3%81%99%E3%82%8B%E6%96%B9%E6%B3%95%E3%81%AF%EF%BC%9F/1046990477/
- https://stackoverflow.com/questions/24386657/how-to-add-a-open-git-bash-here-context-menu-to-the-windows-explorer

#### レジストリ操作全般

（何かあったときに後で修正出来るようメモ）
- https://thinkit.co.jp/story/2015/06/30/6147
- https://weekly.ascii.jp/elem/000/001/505/1505132/
- https://www.lifehacker.jp/2016/01/160125_rightclick_menu.html
- https://ascii.jp/elem/000/000/953/953807/
- https://qiita.com/NumLocker/items/f8016f1aed7207b850fb
- https://laboradian.com/add-item-to-context-menu/
- https://freesoft-100.com/pasokon/context.html
- https://www.atmarkit.co.jp/ait/articles/0511/19/news016.html

#### workspace

(HOMEディレクトリから開始出来るようにしておく)
- https://www.granfairs.com/blog/staff/gitbash-setting-shortcut

