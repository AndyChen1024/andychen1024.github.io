# 通过Github Actions打包Apk到蒲公英


1. #### [Github Actions](https://docs.github.com/cn/actions)

主要处理的yml文件示例：

```yml
# workflow的名称，会显示在github 的项目的Actions的右边列表中，如下图
name: Android CI
#处理的分支，一般是master或者release相关的，dev好像搞不了
on:
  push:
    branches: 
      - master
  pull_request:
    branches: 
      - master

jobs:
  build:
#设置该job 运行的系统环境，支持ubuntu 、windows、macOS
    runs-on: ubuntu-latest
#step:我项目是jdk11的所以设置了11
    steps:
    - uses: actions/checkout@v2
    - name: set up JDK 11
      uses: actions/setup-java@v2
      with:
        java-version: '11'
        distribution: 'temurin'
        cache: gradle

    - name: Grant execute permission for gradlew
      run: chmod +x gradlew
    - name: Build with Gradle
      run: ./gradlew assembleDebug

    #step：上传apk 到action，在右上角查看
    # 官方文档 https://help.github.com/cn/actions/automating-your-workflow-with-github-actions/persisting-workflow-data-using-artifacts#uploading-build-and-test-artifacts
    - name: Upload APK
      uses: actions/upload-artifact@v1
      with:
          name: app
          path: app/build/outputs/apk/debug/app-debug.apk

    # step：向蒲公英上传文件
    - name: Upload To Pgyer
      uses: JantHsueh/upload-file-action@master
      with:
          url: https://www.pgyer.com/apiv2/app/upload
          method: POST
          # ${{ secrets.pgyer_key }} 使用秘钥，秘钥在github的setting中设置
          forms: '{"_api_key":"${{ secrets.learn_app_secret }}","buildInstallType":3}'
          fileForms: '{"file":"app/build/outputs/apk/debug/app-debug.apk"}'480
```

