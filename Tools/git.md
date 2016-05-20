配置信息
`git config --global user.name 'Demo'`      
`git config --global user.email 'Demo.demo.com'`    
`git config -e` 编辑全局变量    
`git config --unset --global user.name` 删除信息  

`git log --pretty=fullyer`  提交日志  
`git log --stat`  每个提交的文件变更统计  

* 创建版本  `git init`    
* 添加文件并提交 `git add -A  `      `git commit -m`  
* 建立里程碑  `git tag v1`    
* 提交修改文件  `git commit -a`  
* 撤销上传文件  `git rm --cached file.md`  

`git add -u` 用户修改过的文件放到暂存区  
`git add -A` 用户删除和修改过的文件放到暂存区  

### 克隆项目  
`git clone git://....x.git`    
`git fetch`  获取最新版本  
`git clean --fdx` 清理遗留文件  
`git reset --hard` 放弃本地对git的修改  
`git checkout ..` 检出代码  






