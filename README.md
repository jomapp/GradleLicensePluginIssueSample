# GradleLicensePluginIssueSimple
Simple project to reproduce an issue in the gradle-license-plugin.

Please see the **build.gradle** file for the task to run in order to reporduce the issue.

```
licenseReport {
    generateHtmlReport = false
    generateJsonReport = true
    copyHtmlReportToAssets = false
    copyJsonReportToAssets = false
}

task generateLicenses { // Does Work ✅
    dependsOn 'licenseDebugReport'
}

task createEmptyLicenseReportIssue { // Does not work ⛔️
    dependsOn 'processDebugManifest'
    dependsOn 'generateLicenses'
}

generateLicenses.mustRunAfter('processDebugManifest')
```

Running **generateLicenses** works correctly and produces the correct json file.

Running **createEmptyLicenseReportIssue** instead produces an **empty json file** and therefore doens't work!
