# GradleでJacocoでレポート出力

<div><p>GradleでJaCoCoを動かすだけならapply pluginにjacocoを追加するだけでいいんですが意外とレポートとして出力する記事が無かったので備忘録。<br>build.gradleファイルに下記を追加することでbuildフォルダ配下の指定の場所にレポートが生成されます。
</p><p>実行時のコマンドは gradle test jacocoTestReport です。<br>
</p><pre class="hljs bash">apply plugin: <span class="hljs-string">'jacoco'</span>
jacocoTestReport {
    group = <span class="hljs-string">"Reporting"</span>
    description = <span class="hljs-string">"Generate Jacoco coverage reports after running tests."</span>
    additionalSourceDirs = files(<span class="hljs-built_in">source</span>Sets.main.allJava.srcDirs)
    reports {
        xml.enabled <span class="hljs-literal">false</span>
        csv.enabled <span class="hljs-literal">false</span>
        html.destination <span class="hljs-string">"<span class="hljs-variable">${buildDir}</span>/reports/jacoco"</span>
        <span class="hljs-built_in">source</span>Sets <span class="hljs-built_in">source</span>Sets.main
    }
}
</pre></div>