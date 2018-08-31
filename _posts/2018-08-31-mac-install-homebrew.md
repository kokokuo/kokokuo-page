---
layout: post
title: "Homebrew (1) - Mac 上安裝 Homebrew 套件管理工具"
categories: 
  - homebrew
tags:
  - mac
  - homebrew
---
## 步驟一：安裝 Homebrew 

Homebrew 是 Mac 專用的套件管理工具，如同 Linux 中的 apt 或是 yum 工具，許多的套件工具都可以透過 Homebrew 安裝，並且管理（如列出安裝的套件、更新套件、修正套件、移除套件等等）

而安裝步驟非常簡單，進入 Homebrew 官網，依照步驟，在 Terminal 輸入下列此串：

```bash
$> /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

<!-- more -->

![安裝 Homebrew](/static/posts/mac-install-homebrew/1-install-homebrew-on-mac.png)

## 步驟二：設定環境變數 PATH

安裝完後，為了要使 Homebrew 的指令可以被 Mac 的 Terminal 中的 Bash 程式讀取到，需要設定 `/usr/local/bin` 與 `/usr/local/sbin` 至環境變數。

建立一個 `.bash_profile` 或是 `.profile` （如果已有其中一個檔案則不需再次建立）並且在檔案中新增此行：

```bash
export PATH=/usr/local/bin:/usr/local/sbin:$PATH
```

或是可以透過 Shell 的另一種語法雙引號來設定

```bash
export "PATH=/usr/local/bin:/usr/local/sbin:$PATH"
```

設定完成後，關閉 Terminal 應用程式重開 或是直接在 Terminal 中輸入以下指令啟動 `.bash_profile` 或 `.profile` 啟動即可（以下以 `.bash_pofile` 為例 ）：

```bash
$> source ~/.bash_pofile
```

如果原先的 Mac 中預設環境變數已有其中一個路徑，或是兩個皆有，則可以只需要把剩餘沒有的補上即可。
例如我的 Mac 透過 export 指令發現環境中缺少 `/usr/local/sbin`：

![export 檢查環境變數](/static/posts/mac-install-homebrew/2-check-export-env.png)

則編輯 `~/.bash_profile`，如下圖：

![編輯 edit_profile](/static/posts/mac-install-homebrew/3-edit-bash-profile.png)

完成後，重新開啟 Terminal 應用程式，再次透過 export 檢查，輸入了 `/usr/local/sbin` ：

![查看環境變數](/static/posts/mac-install-homebrew/4-export-new-env.png)

## 步驟三：測試 brew 指令

可以透過輸入 brew 來做所有跟 Homebrew 有關的套件管理操作行為，如下圖：

如診斷：
![測試 brew 指令](/static/posts/mac-install-homebrew/5-test-brew.png)

## 安裝套件：以 wget 為例
以下透過安裝 wget 套件為例， wget 可以用來直接在終端機上安裝網路上的檔案內容，輸入：

```bash
$> brew install
```

![安裝 wget](/static/posts/mac-install-homebrew/6-ex-install-wget.png)

## Homebrew 資料夾目錄介紹：

如上述所提到的環境變數設定，Homebrew 安裝完後，會放在 `/usrl/local` 下，而 Homebrew 下載安裝或管理套件，會影響到  `/usrl/local`  下這幾個目錄：

```
Caskroom  Frameworks  bin  include  opt   share
Cellar    Homebrew    etc  lib      sbin  var
```

`Cellar`：文件夾存放的是所有包安裝所在路徑，包括二進制，文檔和配置文件。依照一下形式放置：按照這樣 

```
Cellar/套件名稱/版本號/
```

`opt`：由於版本號隨著跟新而改變的，所以需要一個固定不變的路徑作為我們訪問二進制和文檔的路徑，這就是 op t的作用。

`Homebrew`：brew 程序所在路徑.

`bin`：所有包安裝之後二進制都會鏈接到這個路徑下

`share`：所有包安裝之後的文檔都會鏈接到這個路徑下

`etc`：同上，所有套件的配置文件

`lib`：同上，所有套件相關庫文件

`Caskroom`：使用 Homebrew Cask 安裝的應用程式 app 的相關資訊或設定的文件

## 參考文件：
[1.Homebrew总结](https://www.jianshu.com/p/8ad7056b243f)