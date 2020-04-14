# README

This README would normally document whatever steps are necessary to get the
application up and running.

Things you may want to cover:

* Ruby version

* System dependencies

* Configuration

* Database creation

* Database initialization

* How to run the test suite

* Services (job queues, cache servers, search engines, etc.)

* Deployment instructions

* ...

## users table                                                        <!--ユーザーに関するテーブル>
|Column|Type|Options|                                                 <!--|カラム|カラム型|カラムのオプション|>
|------|----|-------|
|name|string|null: false, foreign-key: true|                          <!--|名前|文字列|空の値×, 外部キー制約|>
|email|string|null: false, unique: true|                              <!--|メール|文字列|空の値×, 一意性制約|>
|password|string|null: false|                                         <!--|パスワード|文字列|空の値×|>

### Association
has_many :messages                                                    <!--一対多>
has_many :groups_users                                                <!--中間テーブル>
has_many :groups, through: :groups_users                              <!--中間テーブルを通してgroupsテーブルとアソシエーション>


## message table                                                      <!--メッセージに関するテーブル>
|Column|Type|Options|                                                 <!--|カラム|カラム型|カラムのオプション|>
|------|----|-------|
|message|string|null: false|                                          <!--|メッセージ|文字列|空の値×|>
|image|text|                                                          <!--|画像|テキスト|>
|user_id|integer|foreign_key: true|                                   <!--|ユーザーid|整数|外部キー制約|>
|group_id|integer|foreign_key: true|                                  <!--|グループid|整数|外部キー制約|>

### Association
belongs_to :user                                                      <!--一対多>
belongs_to :group                                                     <!--一対多>


## groups table                                                       <!--グループに関するテーブル>
|Column|Type|Options|                                                 <!--|カラム|カラム型|カラムのオプション|>
|------|----|-------|
|groupname|string|null: false|                                        <!--|グループ名|文字列|空の値×|>

### Association
has_many :messages                                                    <!--一対多>
has_many :groups_users                                                <!--中間テーブル>
has_many :users, through: :groups_users                               <!--中間テーブルを通してusersテーブルとアソシエーション>


## groups_users table                                                 <!--groupsとusersの中間テーブル・・・多対多を防ぐ>
|Column|Type|Options|                                                 <!--|カラム|カラム型|カラムのオプション|>
|------|----|-------|
|user_id|integer|null: false, foreign_key: true|                      <!--|ユーザーid|文字列|空の値×, 外部キー制約|>
|group_id|integer|null: false, foreign_key: true|                     <!--|グループid|文字列|空の値×, 外部キー制約|>

### Association
belongs_to :group                                                     <!--一対多>
belongs_to :user                                                      <!--一対多>
