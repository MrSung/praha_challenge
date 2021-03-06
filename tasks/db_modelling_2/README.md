# DB モデリング２

## 課題１

横断機能

- メッセージとスレッドメッセージを横断的に検索できること（例えば「hoge」と検索したら、この文字列を含むメッセージとスレッドメッセージを両方とも取得できること）
- 参加していないチャネルのメッセージ・スレッドメッセージは検索できないこと

> **Note:**
>
> - 投稿されたメッセージ`MESSAGE`に紐付いている、`MESSAGE-CONTENT`のスレッド ID `thread_id` は、スレッドの生成の際に用いられる
>   - 同じスレッド内のメッセージは、同じスレッド ID を持つ
>   - 同じスレッド ID のうち、メッセージ投稿日時 `message_posted_at` の一番古いものが親メッセージとして用いられる
> - メッセージなど、頻繁に変更が発生するものに関しては、基本は論理削除を想定している
> - ユーザーのワークスペース・チャンネルへの参加・脱退の際は、中間テーブルである`USER-PER-WORKSPACE`と`USER-PER-CHANNEL`から、それぞれ、対象のレコードの追加・物理削除をすることで、結びつきを追加することと、切ることに対応する
>   - チャンネルに表示するメッセージは、メッセージ種別 `message_context` の値を `SYSTEM` に指定することで出し分ける
> - スレッドメッセージは、実際の挙動で確認したところ、親のメッセージを削除しても存在する

[![課題１のER図](https://mermaid.ink/img/pako:eNq1ld9qE0EUxl9lmOvkBfYupFuV2nTpRkRYCNPd02RxdybsTlBJemEGxRYK3pRS70RbWpRWEMSg4MMMSfEtnNnsvyZZWgpeJAxzfud833zJzg6xyzzABoZozSfdiIQOdejTre0N22o0TTQa1etsiJoPG62W-RgZyGWUE5_GDn1im9tZXa_rlvoUnQbagYDRbtzhrAIuppbRJfFbh2dz7jZ_gd40bbvxwKw8WlHvs5irYrah66NRVq83t1pts9VWXI_EOsRkyNChCLk9EhGXQ4QGMUQd30PWBnKwFGdS_JbjH-r70ZqDNcrhJZ9TlISwAE3fH2pqbz57IZIKpfUqpQJ9waLncZ-4UOKvEv5KjidSfEjWk3ljWTxL8v7SakUpBCX6tRSfpPguxaEUX3LJymPe8G7d4j2Nt-jJM17RUoRdccySd6vS-71zTr1mIrnTGxqFx-xPueAxhDgm3XI4H6UQcvwrkfq57PE__HaLD0i1xfU7WeS9CIineQXr3L5qXuxnJNBBmE_Vz7TOcWnu9fnl9N2pkVwWNWQ_s9vmZin3tH-5b_r2zfRykpK-wjgJ-7mcviLA65AVgrODo-vzP7Pj09nJeN6-w1gAhCI_7mT9HgSgBqyQ3T_4e_JZiiMpLuT4WxotruEQopD4nrrBk1wdzHsQgoMNtfRglwwCnsAKHfQ9wsH0fM4ibOySIIYaJgPO7FfUzTfmVPoySHf3_gHMyoeu)](https://mermaid.live/edit#pako:eNq1ld9qE0EUxl9lmOvkBfYupFuV2nTpRkRYCNPd02RxdybsTlBJemEGxRYK3pRS70RbWpRWEMSg4MMMSfEtnNnsvyZZWgpeJAxzfud833zJzg6xyzzABoZozSfdiIQOdejTre0N22o0TTQa1etsiJoPG62W-RgZyGWUE5_GDn1im9tZXa_rlvoUnQbagYDRbtzhrAIuppbRJfFbh2dz7jZ_gd40bbvxwKw8WlHvs5irYrah66NRVq83t1pts9VWXI_EOsRkyNChCLk9EhGXQ4QGMUQd30PWBnKwFGdS_JbjH-r70ZqDNcrhJZ9TlISwAE3fH2pqbz57IZIKpfUqpQJ9waLncZ-4UOKvEv5KjidSfEjWk3ljWTxL8v7SakUpBCX6tRSfpPguxaEUX3LJymPe8G7d4j2Nt-jJM17RUoRdccySd6vS-71zTr1mIrnTGxqFx-xPueAxhDgm3XI4H6UQcvwrkfq57PE__HaLD0i1xfU7WeS9CIineQXr3L5qXuxnJNBBmE_Vz7TOcWnu9fnl9N2pkVwWNWQ_s9vmZin3tH-5b_r2zfRykpK-wjgJ-7mcviLA65AVgrODo-vzP7Pj09nJeN6-w1gAhCI_7mT9HgSgBqyQ3T_4e_JZiiMpLuT4WxotruEQopD4nrrBk1wdzHsQgoMNtfRglwwCnsAKHfQ9wsH0fM4ibOySIIYaJgPO7FfUzTfmVPoySHf3_gHMyoeu)
