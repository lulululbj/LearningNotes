1. `gitignore` 失效

已经 `add` 的文件再加入 `.gitignore` 会无效，需要删除缓存

```
git rm -r --cached .  
git add .
git commit -m "update gitignore"
```
