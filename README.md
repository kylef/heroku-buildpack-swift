# Heroku buildpack: swift

This is a Heroku buildpack for Swift apps that are powered by the Swift Package Manager.

Check out the [Curassow-example-helloworld](https://github.com/kylef/Curassow-example-helloworld)
for a fully working example that can be deployed to Heroku.

## Usage

Example usage:

```shell
$ ls
Procfile Package.swift Sources

$ heroku create --buildpack kyle/swift

$ git push heroku master
remote: -----> Swift app detected
remote: -----> Installing Swift 4.1
remote: -----> Installing clang-3.7.0
remote: -----> Building Package
remote: -----> Copying binaries to 'bin'
```

You can also add it to upcoming builds of an existing application:

```shell
$ heroku buildpacks:set kyle/swift
```

The buildpack will detect your app as Swift if it has a `Package.swift` file in
the root.

### Procfile

Using the Procfile, you can set the process to run for your web server. Any
binaries built from your Swift source using swift package manager will
be placed in your $PATH.

```swift
web: HelloWorld --workers 3 --bind 0.0.0.0:$PORT
```

### Specify a Swift version

You can also customise the version of Swift used with a `.swift-version` file
in your repository:

```shell
$ cat .swift-version
4.1
```

The `.swift-version` file is completely compatible with
[swiftenv](http://github.com/kylef/swiftenv).

**NOTE**: *Since there are frequent Swift language changes, it's advised that
you pin to your Swift version.*

### Hooks

You can place custom scripts to be ran before and after compiling your Swift
source code inside the following files in your repository:

- `bin/pre_compile`
- `bin/post_compile`

This is useful if you would need to install any other dependencies.

## Using the latest buildpack code

The `kyle/swift` buildpack from the [Heroku Registry](https://devcenter.heroku.com/articles/buildpack-registry) represents the latest stable version of the buildpack. If you'd like to use the latest buildpack code from this Github repository, you can set your buildpack to the Github URL:

```sh-session
$ heroku buildpacks:set https://github.com/kylef/heroku-buildpack-swift
```
