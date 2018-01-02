# Automating your company with fastlane!

## Fastlane

- Keep your signing keys in-sync with git

https://codesigning.guide

### [once] User for managing apps & certificates
1. Register a new user Apple Developer Portal (deploy-bot@thunder.com)
2. Invite user on Apple Developer Portal (as Admin)
3. Invite user on iTunes Connect (as Manager)
4. Create repository for certificates and signing profiles on GitHub
5. Create separate User on github with RW access to the repo above 

### [once] fastlane setup
1. Install bundler
```
sudo gem install bundler
```

2. Init bundle on ios
```
cd ios
bundle init
```

3. Init bundle on android
```
cd android
bundle init
```

4. Add fastlane to both ios and android Gemfiles
```
gem "fastlane"
```

5. Install fastlane (for both iOS and Android)
```
bundle update
```

## iOS

### Info.plist
Add this to `Info.plist`
```
	<key>ITSAppUsesNonExemptEncryption</key>
	<false/>
```

### Creating App on iTunes Connect & Apple developer portal

```
$ cd ios
$ bundle exec fastlane produce
```
- Select team (if you have multiple)
- Provide username, bundle identifier & app name

### Init new fastlane config file
```
$ cd ios
$ bundle exec fastlane init
```


### Manage Signing
```
$ cd ios
$ bundle exec fastlane match init
```
Pass the ssh url of your GitHub's repo

Generate distribution signing identity
```
$ cd ios
$ bundle exec fastlane match appstore
```

Generate development signing identity
```
$ cd ios
$ bundle exec fastlane match development
```


XCode:
- Disable Automatically manage signing (Both targets)
- Select the debug and release signing
- Go to build settings tab, type code signing
- Debug -> iPhone Developer: ...
- Release -> iPhone Release: ...

Then test the release build:
```
$ cd ios
$ xcodebuild clean build -workspace $ProjectName.workspace -configuration Release -scheme $ProjectScheme
```
