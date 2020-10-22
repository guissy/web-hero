# 项目分析工具
## git
```shell script
git whatchanged --author="钟履桂" --diff-filter=A --no-commit-id --name-only --since='2019-10-17' | grep js$ | xargs
```
## 代码分析
[gitinspector](https://github.com/ejwa/gitinspector)
```shell script
gitinspector -lmrTw src
```
## 代码行数
[cloc](https://github.com/AlDanial/cloc)
```shell script
cloc src
```
## 复杂度
[eslintcc](https://github.com/eslintcc/eslintcc)
```shell script
eslintcc -r=all -sr -a src/**/*.*
```
## 重复检查
[jscpd](https://github.com/kucherenko/jscpd)
```shell script
jscpd src
```
