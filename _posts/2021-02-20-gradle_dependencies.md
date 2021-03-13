---
{"layout": "post", "categories": "Installation", "title": "gradle dependencies", "feature-img": "assets/img/feature_img.png"}
---
# dependency 설정
```
dependencies {
    compile group: 'commons-io', name: 'commons-io', version: '2.4'
    if (org.gradle.internal.os.OperatingSystem.current().isLinux()) {
        compile fileTree(dir: 'lib/hdf5/linux', include: '*.jar')
        runtime fileTree(dir: 'lib/hdf5/linux', include: '*.so')
    } else {
        compile fileTree(dir: 'lib/hdf5/win64', include: '*.jar')
        runtime fileTree(dir: 'lib/hdf5/win64', include: '*.dll')
    }
    testCompile group: 'junit', name: 'junit', version: '4.12'
}
```
