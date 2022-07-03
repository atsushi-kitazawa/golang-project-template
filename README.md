## このリポジトリは？

Go言語のプロジェクトテンプレートです。

## 環境作成

以下の環境で開発を実施します。
後述の手順に従って環境を作成してください。

### [環境情報]
* Windows 10
* Visual Studio Code
* Go 1.18
* Git 

1. Visual Studio Codeをインストールする

    以下サイトから Windows のインストーラをダウンロードし、インストールしてください。

    [Download Visual Studio Code - Mac, Linux, Windows](https://code.visualstudio.com/download)

2. Goをインストールする

    以下サイトから Windows のインストーラをダウンロードし、インストールしてください。
    なお、利用するバージョンは 1.18.x 系としてください。

    インストール後、`go` コマンドが実行できることを確認してください。

    [Downloads - The Go Programming Language](https://go.dev/dl/)

3. Gitをインストールする
   
    以下サイトから Windows のインストーラをダウンロードし、インストールしてください。
    最新バージョンで問題ありません。
    
    インストール後、`git` コマンドが実行できることを確認してください。

    [Git - Downloading Package](https://git-scm.com/download/win)

4. リポジトリをクローンする

    このリポジトリをクローンしてください。
    ```
    > git clone https://github.com/atsushi-kitazawa/golang-project-template.git
    ```

5. Visual Studio Code を起動する

    クローンしたディレクトリに移動して Visual Studio Code を起動してください。
    ```
    > cd golang-project-template
    > code .
    ```

    起動後、画面右下に拡張をインストールする旨のダイアログが表示されるので `install` をクリックしてください。

6. Hello World を書いてみる

    `Hello World` と出力するアプリを書いてみます。
    `cmd` というディレクトリを作成し、その配下に `hello.go` というファイルを作成してください。

    `hello.go` の内容は次の通りとしてください。
    ```go
    package main

    import "fmt"

    func main() {
	    fmt.Println("Hello World")
    }
    ```

    コマンドプロンプトで以下の通り入力して、`Hello World` と表示されることを確認してください。
    ```
    > go run cmd\hello.go
    hello world.
    ```

7. サードパーティ製モジュールを利用してみる

    サードパーティ製モジュールを利用する方法も記載しておきます。
    ここでは `Gin` という Webフレームワークを利用してみます。

    [gin-gonic/gin](https://github.com/gin-gonic/gin)

    プロジェクトディレクトリで以下のように入力してください。
    ```
    > go mod init example.com/mytest
    > go get -u github.com/gin-gonic/gin
    ```

    `hello.go` を以下のように書き換えてください。

    ```go
    package main

    import (
	    "net/http"

	    "github.com/gin-gonic/gin"
    )

    func main() {
	    r := gin.Default()
	    r.GET("/ping", func(c *gin.Context) {
		    c.JSON(http.StatusOK, gin.H{
			    "message": "pong",
		    })
	    })
	    r.Run() // listen and serve on 0.0.0.0:8080 (for windows "localhost:8080")
    }
    ```

    以下のコマンドで依存関係ライブラリの更新を行います。
    ```
    > go mod tidy
    ```

    実行します。
    ```
    > go run cmd\hello.go
    ```

    ブラウザから `http://localhost:8080/ping` へアクセスし `{"message":"pong"}` と表示されれば成功です。