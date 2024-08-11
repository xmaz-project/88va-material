## リポジトリの書設定

* 文字コード: UTF-8
* 改行: LF

## 環境構築

### rubyのインストール
※ Windows + WSL2 の例

[この解説](https://qiita.com/tsukamoto/items/6e9a181b6e0defc27a39)に従い以下をインストール。
- rbenv
- ruby 2.7.8
- bundler

サマリー

```
git clone https://github.com/rbenv/rbenv.git ~/.rbenv
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(rbenv init -)"' >> ~/.bashrc

※ ここで ubuntu にログインしなおし

mkdir -p "$(rbenv root)"/plugins
git clone https://github.com/rbenv/ruby-build.git "$(rbenv root)"/plugins/ruby-build

sudo apt install build-essential
sudo apt-get install -y libssl-dev libreadline-dev zlib1g-dev

rbenv install --list-all
⇒ 2.7.8 があることを確認

rbenv install 2.7.8
rbenv global 2.7.8
ruby -v
⇒ ruby 2.7.8p225 (2023-03-30 revision 1f4d455848) [x86_64-linux]

gem list
⇒ bundler (default: 2.1.4) があることを確認
```


### ライブラリインストール

```
make install
```

## 各種操作

表示確認用のローカルサーバ起動

```
make serve  
```

ブラウザで以下にアクセス

```
http://127.0.0.1:4000/88va-material/
```