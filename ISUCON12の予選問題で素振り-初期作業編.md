# ISUCON12の予選問題で素振り（初期作業編）

- https://github.com/matsuu/cloud-init-isucon/
- https://github.com/matsuu/cloud-init-isucon/tree/main/isucon12q

## 初期作業

- [install-app.sh](https://github.com/hiroyasuhajime/scripts?tab=readme-ov-file#install-appsh) の実行
- kataribeとか諸々が入る

## GitHub用のkey設定

```
ssh-keygen -t ed25519 -f ~/.ssh/id_ed25519 -N ""
sudo cat ~/.ssh/id_ed25519.pub
```

https://github.com/settings/ssh/new

## gitの設定

```
cd ~
git clone git@github.com:tkancf-sandbox/isucon12q.git
mv isucon12q/.git* .
rm isucon12q/README.md
rmdir isucon12/
git config --global user.name "tkancf"
git config --global user.email "tkancf@isucon"
git config --global core.editor vim
git add .
git commit -m "ISUCON Start!!!"
```

## nginx, mysqlをgitディレクトリに追加

```
mkdir nginx
cp -a /etc/nginx/sites-available/isuports.conf nginx/isuports.conf
cp -a /etc/nginx/nginx.conf nginx/nginx.conf
mkdir mysqld
cp -a /etc/mysql/mysql.conf.d/mysqld.cnf  mysqld/mysqld.cnf
ll /etc/mysql/mysql.conf.d/mysqld.cnf /etc/nginx/sites-available/isuports.conf /etc/nginx/nginx.conf
git add .
git commit -m "Add middleware conf files"
```

## 最初のベンチマークを実行
```
$ cd bench
$ ./bench -target-addr 127.0.0.1:443
.
.
.
13:08:08.279077 Error 0 (Critical:0)
13:08:08.279079 PASSED: true
13:08:08.279081 SCORE: 3472 (+3472 0(0%))
```

# nginxの設定

Vimでnginxのconf開いたときにフォーマットがムカつくときの対処法

```
set expandtab tabstop=4 shiftwidth=4 softtabstop=4
```

nginxのLogFormatを設定

https://github.com/tkancf-sandbox/isucon12q/commit/dde7a77886cd3320d0e9c56d11f901c57ad82175
[kataribeのREADME](https://github.com/matsuu/kataribe) を参照した

# MySQLの設定

```
mysql-sloq-on.sh
```

# 設定後のベンチマークを実行して analyze

```
prepare.sh
bench.sh
analyze.sh
```
