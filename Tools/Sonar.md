# Sonarqube
 
## 默认端口：
localhost:9000/


## sonar-runner

(需要安装js,css,web插件)
* 1.到updateCenter自动下载安装
* 2.手动下载插件放到SonarHome/extensions/plugins/


sonar-project.properties
```
sonar.projectKey=wxzj_html
sonar.projectName=wxzj_html
sonar.projectVersion=1.0
sonar.sourceEncoding=UTF-8
sonar.modules=js,css,html  

js.sonar.projectName=JS Module  
js.sonar.language=js  
js.sonar.sources=js
js.sonar.projectBaseDir=public


css.sonar.projectName=CSS Module  
css.sonar.language=css  
css.sonar.sources=css  
css.sonar.projectBaseDir=public

html.sonar.projectName=HTML Module  
html.sonar.language=web  
html.sonar.sources=.
html.sonar.projectBaseDir=views
```
