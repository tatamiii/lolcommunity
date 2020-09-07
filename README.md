# README

# アプリケーション名	lolcommunity

# アプリケーション概要
# 世界において1億人以上のユーザー数を誇るLeague of Legend(PCオンラインゲーム)だが、
# 日本において現在アクティブなコミュニティサイトが存在しない。
# ないなら自分で作る、という気持ちで作成を行った。
# ユーザー登録を行うことができ、掲示板で匿名、非匿名でのコミュニケーションを行うことができる他、
# 一緒に遊ぶ友人を探すことのできる機能の実装を目指す。

# URL	https://github.com/tatamiii/lolcommunity

# テスト用アカウント	未実装

# 利用方法
# ①ユーザー登録機能       下記の機能の利用の際、ユーザーを識別するために実装する。
# ②掲示板機能             スレッドを立ち上げて、その内容について議論を行うことができる。
#                          匿名、非匿名どちらでも機能の利用は行える。
# ③Duoパートナー検索機能  ユーザー登録した情報を元に、実力の近いユーザー同士をマッチングさせて
#                          一緒の試合を行えるよう手配を行う。可能であれば終了時に相手に対して
#                          評価を行う機能の実装も行う。
# ④Build投稿機能          ユーザー登録した人のみ投稿可能
#                          自身の得意とするキャラクターのガイドやマッチアップ解説を行う。
#                          投稿に対し、ユーザーがGood or Badの評価やコメントを行うことができる。

# 目指した課題解決
# 世界において1億人以上のユーザー数を誇るLeague of Legend(PCオンラインゲーム)だが、
# 日本において現在アクティブなコミュニティサイトが存在しない。
# ないなら自分で作る、という気持ちで作成を行った。
# ユーザー登録を行うことができ、掲示板で匿名、非匿名でのコミュニケーションを行うことができる他、
# 一緒に遊ぶ友人を探すことのできる機能の実装を目指す。


# 実装した機能についてのGIFと説明	現在未実装

# 実装予定の機能	利用方法に記述した物全て(優先順位は上のほうが高い)

# テーブル設計

## users テーブル

| Column        | Type   | Options     |
| ------------- | ------ | ----------- |
| name          | string | null: false |
| email         | string | null: false |
| password      | string | null: false |
| summoner_name | text   |             |
| current_rate  | text   |             |

- has_many :rooms
- has_many :rooms_messages
- has_many :guides


## rooms(掲示板) テーブル

| Column          | Type       | Options     |
| --------------- | ---------- | ----------- |
| title(タイトル) | string     | null: false |
| text(本文)      | text       | null: false |
| Poster(投稿者)  | references | null: false |

### Association

- has_many :room_messages


## room_messages テーブル

| Column   | Type       | Options                        |
| -------- | ---------- | ------------------------------ |
| message  | references | null: false                    |
| user     | references | null: false, foreign_key: true |
| room     | references | null: false, foreign_key: true |

### Association

- belongs_to :user
- belongs_to :room


## guides テーブル

| Column   | Type       | Options                        |
| -------- | ---------- | ------------------------------ |
| user     | references | null: false, foreign_key: true |
| title    | text       | null: false                    |
| text     | text       | null: false                    |

### Association

- belongs_to :user
