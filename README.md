# AndroidPackagingConfiguration

### Gradle自定义apk名称报错
- ERROR: Cannot set the value of read-only property 'outputFile' for ApkVariantOutputImpl_Decorated{apkData=Main{type=MAIN, fullName=my_appRelease, filters=[], versionCode=1, versionName=1.0}} of type com.android.build.gradle.internal.api.ApkVariantOutputImpl.
```
    applicationVariants.all { variant ->
           variant.outputs.each { output ->
               def fileName = "${variant.versionName}_${variant.productFlavors[0].name}" + releaseTime() + ".apk"
               def outFile = output.outputFile
               if (outFile != null && outFile.name.endsWith('.apk')) {
                   output.outputFile = new File(outFile.parent, fileName)
               }
           }
       }
```
==改为==
```
 applicationVariants.all { variant ->
        variant.outputs.all { output ->
            def fileName = "${variant.versionName}_${variant.productFlavors[0].name}" + releaseTime() + ".apk"
            def outFile = output.outputFile
            if (outFile != null && outFile.name.endsWith('.apk')) {
                outputFileName = fileName
            }
        }
    }
    
```

- All flavors must now belong to a named flavor dimension.

```
flavorDimensions "code"
```

- WARNING: API 'variantOutput.getPackageApplication()' is obsolete and has been replaced with 'variant.getPackageApplicationProvider()'.
  It will be removed at the end of 2019
 
 ```
 classpath 'com.android.tools.build:gradle:3.2.1'
 ```