# proc maps parser Prefab

Prefab package for <https://github.com/ouadev/proc_maps_parser>.

## Changes to original

- Don't use temporary buffers (from https://github.com/RikkaApps/Riru/pull/202)
- Add `extern "C"` in `pmparser.c
- Use name "proc-maps-parser" instead of "pmparser", since in Android, "pm" is the very common abbreviation for "PackageManager"

## Integration

This is a [Prefab](https://google.github.io/prefab/) library, so you will need to enable it in your project (requires Android Gradle Plugin 4.1+):

```gradle
android {
    ...
    buildFeatures {
        ...
        prefab true
    }
}
```

Add dependency:

```gradle
repositories {
    mavenCentral()
}

dependencies {
    implementation 'dev.rikka.ndk.thirdparty:proc-maps-parser:1.0.0'
}
```

## Usage

### ndk-build

```makefile
LOCAL_STATIC_LIBRARIES := proc-maps-parser

# You can remove this block if you are using NDK r21+.
ifneq ($(call ndk-major-at-least,21),true)
    $(call import-add-path,$(NDK_GRADLE_INJECTED_IMPORT_PATH))
endif

$(call import-module,prefab/proc-maps-parser)
```

### CMake

```cmake
find_package(proc-maps-parser REQUIRED CONFIG)
target_link_libraries(<your lib> proc-maps-parser::proc-maps-parser)
```
