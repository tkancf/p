# ISUCON12の予選問題で素振り (一個目の改善 - MySQL)
スロークエリログを集計すると下記コードのクエリが上位に来るのでここから手をつける

```
"SELECT player_id, MIN(created_at) AS min_created_at FROM visit_history WHERE tenant_id = ? AND competition_id = ? GROUP BY player_id",   
```

ISUCONでよくあるのは、schema.sqlでINDEX追加するんだけどISUCON12予選はschemaがinit.shで読まれない = drop tableされないので、手で叩いておけばOK

カバーリングインデックスを追加する。 ([講評を参照](https://isucon.net/archives/56850281.html))
既存のインデックスは削除する

```
ALTER TABLE visit_history DROP INDEX tenant_id_idx;
CREATE INDEX idx_visit_history_cover ON visit_history(tenant_id, competition_id, player_id, created_at);
```
