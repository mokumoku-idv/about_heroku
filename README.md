# about_heroku
paasの一種。プラグインが豊富で、無料枠もそれなりにある
しょぼいものなら、結構無料の範囲でいける
wantedlyはherokuでサービス運用してる

## dyno
サーバみたいなもの

## 使うメリット
以下のページ見た方が、いいが、一番はインフラに回してたコストを減らすことができること

## 初期設定
まずは、初期設定に関して
以下のコマンドで、railsのアプリが作れるよ
```
git clone https://github.com/heroku/ruby-getting-started.git
shhirats% heroku login
Enter your Heroku credentials.
Email: hiratsukashu@indival.co.jp
Password (typing will be hidden):
Authentication successful.
{15-03-19 
19:31}MBP-15JAC-105:~/admin-redirect/ruby-getting-started@master 
shhirats% heroku create
Creating ancient-dawn-3677... done, stack is cedar-14
https://ancient-dawn-3677.herokuapp.com/ | 
https://git.heroku.com/ancient-dawn-3677.git
Git remote heroku added
{15-03-19 
19:31}MBP-15JAC-105:~/admin-redirect/ruby-getting-started@master 
shhirats% git push heroku master
shhirats% heroku ps:scale web=1
Scaling dynos... done, now running web at 1:1X.
{15-03-19 
19:39}MBP-15JAC-105:~/admin-redirect/ruby-getting-started@master 
shhirats% heroku open
Opening ancient-dawn-3677... done
```
## 複数人で開発する場合
以下のページを参考に共有する必要があり
```
https://devcenter.heroku.com/articles/create-manage-org
https://devcenter.heroku.com/articles/sharing
```


## cron
* clockworkとHeroku Schedular
* お金かかっちゃうから、テストは出来んなー。

## 参考
* いろいろ自分で説明するより、こっち見た方が早い
* http://blog.mah-lab.com/2013/05/16/heroku-commons-16/
* http://qiita.com/shu_0115/items/0106198f7a0be2f2a509
