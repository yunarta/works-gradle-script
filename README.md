# works-gradle-script

This is a collection of useful direct apply Gradle scripts.

## Auto Configure

Auto configure Android API level and Build Tools to use the latest available from Google. The script also provide latest Android Support library revision number.

This is primarily useful for Android library source compilation. Most of the case when your library has not been update for quite a while, your will be referring to older API and tools, while Android guideline recommends that you always compile with the latest tools.

What the script do:

1. Check the Android repository for revision informations
2. Save the repository files into temporary if permitted, so only one downloaded daily 
3. If #1 and #2 is not possible, it will use Android SDK directory and scans for the revisions there (this will allow the script to at least use the latest available downloaded)

**Usage**
```
apply from: ('https://raw.githubusercontent.com/yunarta/works_gradle_script/master/auto-configure.gradle')

android {
    compileSdkVersion autoCompileSdkVersion(22)
    buildToolsVersion autoBuildToolsVersion('22.0.1')
}
	
dependencies {
    compile 'com.android.support:support-v13:' + autoSupportLibVersion('23.0.0')
}
```

The value inside the bracket is for fallback in case there is no Internet connection.

## BinTray publish script

BinTray publish script is used to simplify uploading of your library into BinTray.

**BinTray Configuration**

Put your BinTray username and API key inside your local.properties file

```
bintray.user=yunarta-kartawahyudi
bintray.apikey=[your API key]
```

**General Publishing Information**
```
apply from: 'https://raw.githubusercontent.com/yunarta/works-gradle-script/master/publish-works.gradle'

group 'com.mobilesolutionworks'
version '1.0.0'

worksPublish {
    bintray {
        repo = 'bintray repository target'
        name = group + ':' + project.name
    }

    developer {
        id = 'yunarta'
        name = 'Yunarta Kartawahyudi'
        email = 'yunarta.kartawahyudi@gmail.com'
    }

    siteUrl = 'https://github.com/yunarta/works-gradle-script'
    gitUrl = 'https://github.com/yunarta/works-gradle-script.git'
}
```
And lastly put either ot this Gradle script at the end of build.gradle, dependending of what kind of library you'll publishing.

**For publishing Android Library**

```
apply from: 'https://raw.githubusercontent.com/yunarta/works-gradle-script/master/publish-bintray-for-android-lib.gradle'
```

**For publishing Java Library**

```
apply from: 'https://raw.githubusercontent.com/yunarta/works-gradle-script/master/publish-bintray-for-java-lib.gradle'
```


