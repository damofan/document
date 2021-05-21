- 修改git全局名字

```javascript
// 去掉 --global 即：仅仅设置本项目的 git 用户名
git config --global user.name xxx
```

- 查看git配置

```javascript
// 去掉 --local 即：查看本地配置
git config --local --list

```

- 添加tag

```js
git add *
git commit -m "1.0.0"
git tag 1.0.0
git push
git push origin 1.0.0
```

- 清空git提交记录，成为一个新的干净仓库

```
git checkout --orphan latest_branch
git add -A
git commit -am "commit message"
git branch -D master
git branch -m master
git push -f origin master
```

