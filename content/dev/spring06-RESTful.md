+++ 
date = "2020-11-14"
title = "Spring In Action 06 - RESTful API"
tags = ["spring", "java", "spring-in-action" ]
draft = true
+++
Set [project](https://github.com/habuma/spring-in-action-5-samples/tree/master/ch06) to java 8. In ch06 folder, run `mvnw clean package`.

First error:
```log
[ERROR] Failed to execute goal com.github.eirslett:frontend-maven-plugin:1.4:install-node-and-npm (install node and npm) on project tacocloud-ui: Could not install Node: Unable to delete file: C:\Users\yanch\g
itProject\spring-in-action-5-samples\ch06\tacocloud-ui\node\tmp\node-v6.9.1-win-x64\node_modules\npm\node_modules\columnify\node_modules\wcwidth\node_modules\defaults\node_modules\clone\LICENSE -> [Help 1]
[ERROR]
```
what I [found](https://stackoverflow.com/questions/19489720/maven-failed-to-clean-project-failed-to-delete-org-ow2-util-asm-asm-tree).
I exited my apps that possibly scan my system, like listary, and it works.

