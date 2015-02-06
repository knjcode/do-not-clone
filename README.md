# do-not-clone

## Githubに一度pushしたコミットを消すことはできるのか実験

Initial commit  
https://github.com/knjcode/do-not-clone/commit/a9fbd28e130d4a84e616a48654fd518b7f471865

Add new file: a  
https://github.com/knjcode/do-not-clone/commit/fee574173f69de7886d2325c209b6f5cd748a0a6

Add new file: b  
https://github.com/knjcode/do-not-clone/commit/8efd518d8616a5440e1ffd8de3528f04d5b3fa43

```
glgga
* commit 8efd518d8616a5440e1ffd8de3528f04d5b3fa43 (HEAD, master)
| Author: knjcode <knjcode@gmail.com>
| Date:   Sat Feb 7 00:45:26 2015 +0900
|
|     Add new file: b
|
* commit fee574173f69de7886d2325c209b6f5cd748a0a6 (origin/master)
| Author: knjcode <knjcode@gmail.com>
| Date:   Sat Feb 7 00:43:51 2015 +0900
|
|     Add new file: a
|
* commit a9fbd28e130d4a84e616a48654fd518b7f471865
  Author: knjcode <knjcode@gmail.com>
  Date:   Sat Feb 7 00:42:22 2015 +0900

      Initial commit
```

2つ目のコミット Add new file: a のコードに対してコメント

```
git reset --hard HEAD^^ //2つ目と3つ目のコミットを履歴から消す
```

abというファイルをつくり、Initial commitにつづく2件目のコミットとしてコミット

```
git push -f origin master // Githubに強制push
```

その後、元々の3つのコミットすると、アクセス可能

GCしてから強制pushしてみる

```
git gc --aggressive
git prune
git push -f
```

やはり元々の3つのコミットにアクセス可能

さらに、cというファイルをつくり3件目のコミットを実施

再度GCしてからpushしてみる

```
git gc --aggressive
git prune
git push
```

やはりアクセス可能

ローカル側で別ディレクトリにGithubから新たにcloneし直す

さらに、dというファイルをつくり4件目のコミットを実施

```
glgga
* commit 6091d1d331dccfbd10761de300e7d9b7e6ae5dc0 (HEAD, origin/master, origin/HEAD, master)
| Author: knjcode <knjcode@gmail.com>
| Date:   Sat Feb 7 00:57:35 2015 +0900
|
|     Add new file: d
|
* commit 8af13aab367c659202422a8e25345ae1e5eae230
| Author: knjcode <knjcode@gmail.com>
| Date:   Sat Feb 7 00:55:03 2015 +0900
|
|     Add new file: c
|
* commit 90c1b31d742d2fd67c32a8596e617cf870fdeed2
| Author: knjcode <knjcode@gmail.com>
| Date:   Sat Feb 7 00:51:21 2015 +0900
|
|     Add new file: ab
|
* commit a9fbd28e130d4a84e616a48654fd518b7f471865
  Author: knjcode <knjcode@gmail.com>
  Date:   Sat Feb 7 00:42:22 2015 +0900

      Initial commit
```

Githubにpush

```
git push origin master
```

やはりアクセス可能

3ヶ月後に確認してみよう（忘れそう）
