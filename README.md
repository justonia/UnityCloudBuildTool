# Unity Cloud Build Tools
CLI tool for interacting with Unity Cloud Build.

By default, commands output human-readable data. If --json is specified as a root flag
a more detailed JSON response will be outputted (e.g. `unity-cb-tool --json targets list`).

```
NAME:
   unity-cb-tool - A new cli application

USAGE:
   unity-cb-tool [global options] command [command options] [arguments...]

VERSION:
   0.1.0

COMMANDS:
     builds   
     targets  
     help, h  Shows a list of commands or help for one command

GLOBAL OPTIONS:
   --api-key value     Unity API key [$UNITY_API_KEY]
   --org-id value      Unity Organization ID [$UNITY_ORG_ID]
   --project-id value  Unity Project ID [$UNITY_PROJECT_ID]
   --json              If true, output responses in JSON
   --help, -h          show help
   --version, -v       print the version
```

## Commands

### `builds list`

```
NAME:
   unity-cb-tool builds list - List builds

USAGE:
   unity-cb-tool builds list [command options] [arguments...]

OPTIONS:
   --target-id value        Specific target ID or _all for all targets (default: "_all")
   --filter-status value    (queued, sentToBuilder, started, restarted, success, failure, canceled, unknown)
   --filter-platform value  (ios, android, webgl, osx, win, win64, linux)
   --limit value, -l value  If >0 show only the specified number of builds (default: 0)
```

#### Example
```
unity-cb-tool builds list --limit 10

---

Target: windows-x64, (Build #16)
  Status:   success
  Time:     12m15s
  Revision: 9102ca18b98706193a6b9d92d51cab8928bd7b97
  Download: https://unitycloud-build-user-svc-live-build.s3.amazonaws.com/...

Target: macos, (Build #15)
  Status:   success
  Time:     18m1s
  Revision: 9102ca18b98706193a6b9d92d51cab8928bd7b97
  Download: https://unitycloud-build-user-svc-live-build.s3.amazonaws.com/...

(truncated...)
```

### `builds latest`

```
NAME:
   unity-cb-tool builds latest - List latest builds for every build target

USAGE:
   unity-cb-tool builds latest [arguments...]
```

#### Example
```
unity-cb-tool builds latest

---

Target: Windows x64 (id=windows-x64)
  Build:    #16
  Status:   success
  Time:     17m13s
  Revision: 9102ca18b98706193a6b9d92d51cab8928bd7b97
  Download: https://unitycloud-build-user-svc-live-build.s3.amazonaws.com/...

Target: MacOS (id=macos)
  Build:    #15
  Status:   success
  Time:     18m3s
  Revision: 9102ca18b98706193a6b9d92d51cab8928bd7b97
  Download: https://unitycloud-build-user-svc-live-build.s3.amazonaws.com/...
```

### `builds cancel`

```
NAME:
   unity-cb-tool builds cancel - Cancel a build for a build target, or if --all is specified cancel all builds

USAGE:
   unity-cb-tool builds cancel [command options] [arguments...]

OPTIONS:
   --all                        If true, cancel all builds
   --target-id value, -t value  Build target ID
   --build value, -b value      Build number for build target (default: -1)
```

#### Examples

Cancel a specific build.
```
unity-cb-tool builds cancel -t windows-x64 -b 17

---

(no output)
```

Cancel all builds for a specific target.
```
unity-cb-tool builds cancel -t windows-x64 --all

---

(no output)
```

Cancel all builds for all targets.
```
unity-cb-tool builds cancel --all

---

(no output)
```


### `targets list`

```
NAME:
   unity-cb-tool targets list - List all build targets

USAGE:
   unity-cb-tool targets list [arguments...]
```

#### Example

```
unity-cb-tool targets list

---

Target: Windows x64
  ID:        windows-x64
  Enabled:   true
  AutoBuild: true
  Branch:    release
  Unity:     2018.1.2f1

Target: MacOS
  ID:        macos
  Enabled:   true
  AutoBuild: true
  Branch:    release
  Unity:     2018.1.2f1
```
