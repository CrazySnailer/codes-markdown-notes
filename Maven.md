


删除Maven Reposities下的*.lastUpdated

```
cd %userprofile%\.m2\repository
for /r %i in (*.lastUpdated) do del %i
```


Maven 镜像网站（from http://docs.codehaus.org/display/MAVENUSER/Mirrors+Repositories）
还可以查看http://repo1.maven.org/maven2/.meta/repository-metadata.xml

Globally balanced urls for Central

United States, California     http://repo1.maven.org/maven2    

```
    <mirror>
      <id>Central</id>
      <url>http://repo1.maven.org/maven2</url>
      <mirrorOf>central</mirrorOf>
      <!-- United States, St. Louis-->
    </mirror>
```
United Kingdom	http://uk.maven.org/maven2

(this is a globally balanced dns, the same as repo1)

```
     <mirror>
      <id>uk.maven.org</id>
      <url>http://uk.maven.org/maven2</url>
      <mirrorOf>central</mirrorOf>
      <!-- United Kingdom -->
    </mirror>
```

Mirrors Repositories Pushed Directly from Central
United States, North Carolina     http://mirrors.ibiblio.org/pub/mirrors/maven2
```
<mirror>
      <id>ibiblio.org</id>
      <url>http://mirrors.ibiblio.org/pub/mirrors/maven2</url>
      <mirrorOf>central</mirrorOf>
      <!-- United States, North Carolina -->
    </mirror>
```

Independent Proxies of Central

France   http://maven.antelink.com/content/repositories/central/

```
 <mirror>
      <id>antelink.com</id>
      <url>http://maven.antelink.com/content/repositories/central/</url>
      <mirrorOf>central</mirrorOf>
      <!-- France -->
    </mirror>
```

