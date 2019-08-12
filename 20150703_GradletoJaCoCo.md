https://blog.tagbangers.co.jp/ja/2015/07/03/GradletoJaCoCo

# GradleでJacocoでレポート出力

GradleでJaCoCoを動かすだけならapply pluginにjacocoを追加するだけでいいんですが意外とレポートとして出力する記事が無かったので備忘録。
build.gradleファイルに下記を追加することでbuildフォルダ配下の指定の場所にレポートが生成されます。
実行時のコマンドは `gradle test jacocoTestReport` です。
```
apply plugin: 'jacoco'
jacocoTestReport {
    group = "Reporting"
    description = "Generate Jacoco coverage reports after running tests."
    additionalSourceDirs = files(sourceSets.main.allJava.srcDirs)
    reports {
        xml.enabled false
        csv.enabled false
        html.destination "${buildDir}/reports/jacoco"
        sourceSets sourceSets.main
    }
}
```