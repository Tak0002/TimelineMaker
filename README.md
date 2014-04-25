TimelineMaker
===============

cakephpのvendorに入れて呼び出すことを想定したアプリケーションです。
ユーザーが自由にタグをフォローすることが出来るアプリケーションにてフォローしているタグに関連付けられたイベントを取得し、タイムラインを生成します。


想定している構造
----------------------------

CakephpのhasAndBelongsToMany構造でタグが管理されている場合を想定しています。


データベースに

* ユーザーを管理するUser
* イベントを管理するEvent
* タグ名を管理するTag

という３つのテーブルが存在し、

* イベントのタグ付けを管理するEventsTag
* ユーザーがフォローしているタグを管理するUsersTag

の２つのhasAndBelongsToMany構造の中間テーブルが存在することを想定しています。


使い方
-------------------------

vendorに入れて、controlerから呼び出します。

例：

```php
        $timelineMaker = new TimelineMaker($this->Auth->user());
        $events = $timelineMaker->getEvents(1, 'Event.id desc', 10, false);
        $recommends = $timelineMaker->getEvents(1, 'Event.participant desc',3 ,false);
```