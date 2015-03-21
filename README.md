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

* https://devcenter.heroku.com/articles/create-manage-org
* https://devcenter.heroku.com/articles/sharing

## ログイン認証
ここを見るのが早そう

http://ruby-rails.hatenadiary.com/entry/20140801/1406907000

## herokuでステージング環境
以下のページとか参考に試してみる

http://gihyo.jp/dev/serial/01/heroku/0007

## コマンド幾つか

* スケールする量の決定
```
heroku ps:scale web=1
```
上記は1dynoで動くよって証拠。２以上必要なら2dyno

* 現在の状態を確認
```
heroku ps
```

* productionを開く
```
heroku open
```

* rake実行
```
heroku run rake db:migrate
```

## ユーザ管理の作成
以下を見て、さっくり出来た。簡単

* http://ruby-rails.hatenadiary.com/entry/20140801/1406907000
サインアップ機能は、URLを外から見れないようにしたいね。
元から見れないんだけど。URL導線は消してしまおう

## railsのrouteのresource
ちょっとわかりにくいんだよね。以下を見たらちょっとわかった

http://www.rubylife.jp/rails/routing/index5.html

RestfulなURLを自動で生成してくれる仕組み
以下のように書くと
```
resources :blogs
```
以下のURLを生成してくれる（実際の例とは違うけど、気にしないでください）
```
GET    'sample'     => 'books#index'
GET    'sample/:id' => 'books#show'
GET    'sample/new' => 'books#new'
POST   'sample'     => 'books#create'
GET    'sample/:id/edit' => 'books#edit'
DELETE 'sample/:id' => 'books#destroy'
PUT    'sample/:id' => 'books#update'
```
使えるルーティング（URL）は以下のコマンドで確認できる
```
% rake routes
                  Prefix Verb   URI Pattern                     Controller#Action
     csv_shot_urls_index GET    /csv_shot_urls/index(.:format)  csv_shot_urls#index
    csv_shot_urls_upload GET    /csv_shot_urls/upload(.:format) csv_shot_urls#upload
        new_user_session GET    /users/sign_in(.:format)        devise/sessions#new
            user_session POST   /users/sign_in(.:format)        devise/sessions#create
    destroy_user_session DELETE /users/sign_out(.:format)       devise/sessions#destroy
           user_password POST   /users/password(.:format)       devise/passwords#create
       new_user_password GET    /users/password/new(.:format)   devise/passwords#new
      edit_user_password GET    /users/password/edit(.:format)  devise/passwords#edit
                         PATCH  /users/password(.:format)       devise/passwords#update
                         PUT    /users/password(.:format)       devise/passwords#update
cancel_user_registration GET    /users/cancel(.:format)         devise/registrations#cancel
       user_registration POST   /users(.:format)                devise/registrations#create
   new_user_registration GET    /users/sign_up(.:format)        devise/registrations#new
  edit_user_registration GET    /users/edit(.:format)           devise/registrations#edit
                         PATCH  /users(.:format)                devise/registrations#update
                         PUT    /users(.:format)                devise/registrations#update
                         DELETE /users(.:format)                devise/registrations#destroy
              home_index GET    /home/index(.:format)           home#index
               home_show GET    /home/show(.:format)            home#show
                 widgets GET    /widgets(.:format)              widgets#index
                         POST   /widgets(.:format)              widgets#create
              new_widget GET    /widgets/new(.:format)          widgets#new
             edit_widget GET    /widgets/:id/edit(.:format)     widgets#edit
                  widget GET    /widgets/:id(.:format)          widgets#show
                         PATCH  /widgets/:id(.:format)          widgets#update
                         PUT    /widgets/:id(.:format)          widgets#update
                         DELETE /widgets/:id(.:format)          widgets#destroy
                    root GET    /                               home#index
    upload_csv_shot_urls POST   /csv_shot_urls/upload(.:format) csv_shot_urls#upload
           csv_shot_urls GET    /csv_shot_urls(.:format)        csv_shot_urls#index
```
## bootstrapの適用
Gemfileに以下を追加して、bundle install
```
gem 'therubyracer' # javascript runtime。lessをコンパイルするために必要
gem 'less-rails' # Railsでlessを使えるようにする。Bootstrapがlessで書かれているため
gem 'twitter-bootstrap-rails' # Bootstrapの本体
```

ここまでで、サーバ再起動が必要

その後以下のコマンドでインストール
```
rails g bootstrap:install
```

強制的にテーマ適用
```
rails g bootstrap:layout -f
```


### bootstrap reference
* http://blog.scimpr.com/2012/08/25/rails%E3%81%ABtwitter-bootstrap%E3%82%92%E8%A8%AD%E5%AE%9A%E3%81%99%E3%82%8B%EF%BD%9Etwitter-bootstrap-rails/
* http://ruby-rails.hatenadiary.com/entry/20140801/1406818800


## cron
* clockworkとHeroku Schedular
* お金かかっちゃうから、テストは出来んなー。

## 参考
* いろいろ自分で説明するより、こっち見た方が早い
* http://blog.mah-lab.com/2013/05/16/heroku-commons-16/
* http://qiita.com/shu_0115/items/0106198f7a0be2f2a509
* http://railsdoc.com/
