# About this fork
This is my fork of [LibGit2Sharp](https://github.com/libgit2/libgit2sharp) intended for use inside of Unity3D editor.
The reason is that Unity3D's mono stack is stii~ll stuck on a subset of .net 3.5 level, while LibGit2Sharp understandably moved on and bumped minimum required .net profile to 4.0.

## Remarks
This is indended to be used by tools from Unity editor only, not in games/apps. It should work on Windows (x86/x64), Macos X (x86/x64) and Linux (x64 only). Fortunatelly pre-compiled binaries of libgit2 match editor platforms just right.

In order to ease the port and maintainance the [Theraot](https://github.com/theraot/Theraot) library is introduced as dependency. It's MIT licensed just like LibGit2Sharp and gets pulled from nuget.

Tests project is left unchanged. It would be nice to port the tests to run inside unity, but that's not on my priority list.

For now this fork follows vNext branch, but will probably switch to a latest stable in the future.

## Compiling
Myself, I'm just open MonoDevelop and hit compile ;)

## Usage in Unity3D
Copy over LibGit2Sharp.dll, Theraot.Core.dll and NativeBinaries directory into your project and place them under an Editor folder.
Since Unity doesn't support native dll mapping files, you need to:

a) rename them as following

- NativeBinaries/linux/amd64/git2-821131f.so
- NativeBinaries/osx/x86_amd64/git2-821131f.bundle
- NativeBinaries/windows/amd64/git2-821131f.dll
- NativeBinaries/windows/x86/git2-821131f.dll

Replace the suffix with the current one, since it changes with each version of libgit2.
Note that the the file extension changed for macos x. It's not quite correct, but should work.
The actual path doesn't actually matter, unity manages to load them, I split them this way just to avoid name clashes.

b) manually select supported platforms for each native library (editor, o/s and architecture).

# LibGit2Sharp

**LibGit2Sharp brings all the might and speed of [libgit2][libgit2], a native Git implementation, to the managed world of .NET and Mono.**

 [libgit2]: http://libgit2.github.com/

## Prerequisites

 - **Windows:** .NET 4.0+
 - **Linux/Mac OS X:** Mono 3.6+

## Online resources

 - [NuGet package][nuget] (Requires NuGet 2.7+)
 - [Source code][source]

 [nuget]: http://nuget.org/List/Packages/LibGit2Sharp
 [source]: https://github.com/libgit2/libgit2sharp/

## Troubleshooting and support

 - Usage or programming related question? Post it on [StackOverflow][so] using the tag *libgit2sharp*
 - Found a bug or missing a feature? Feed the [issue tracker][tracker]
 - Announcements and related miscellanea through Twitter ([@libgit2sharp][twitter])

 [so]: http://stackoverflow.com/questions/tagged/libgit2sharp
 [tracker]: https://github.com/libgit2/libgit2sharp/issues
 [twitter]: http://twitter.com/libgit2sharp

## Current project status

The CI builds are generously hosted and run on the [Travis][travis] and [AppVeyor][appveyor] infrastructures.

|  | Windows (x86/amd64) | Linux/Mac OS X |
| :------ | :------: | :------: |
| **master** | [![master win][master-win-badge]][master-win] | [![master nix][master-nix-badge]][master-nix] |
| **vNext** | [![vNext win][vNext-win-badge]][vNext-win] | [![vNext nix][vNext-nix-badge]][vNext-nix] |

The security-oriented static code analysis is kindly run through the [Coverity][coverity] service. Code coverage is kindly run through [Coveralls.io][coveralls].

|       | Static Analysis | Code Coverage |
|-------|-----------------|---------------|
| **vNext** | [![coverity][coverity-badge]][coverity-project] | [![coveralls][coveralls-badge]][coveralls-project] |


 [travis]: https://travis-ci.org/
 [appveyor]: http://appveyor.com/
 [coverity]: https://scan.coverity.com/
 [coveralls]: https://coveralls.io/

 [master-win-badge]: https://ci.appveyor.com/api/projects/status/8qxcoqdo9kp7x2w9/branch/master?svg=true
 [master-win]: https://ci.appveyor.com/project/libgit2/libgit2sharp/branch/master
 [master-nix-badge]: https://travis-ci.org/libgit2/libgit2sharp.svg?branch=master
 [master-nix]: https://travis-ci.org/libgit2/libgit2sharp/branches
 [vNext-win-badge]: https://ci.appveyor.com/api/projects/status/8qxcoqdo9kp7x2w9/branch/vNext?svg=true
 [vNext-win]: https://ci.appveyor.com/project/libgit2/libgit2sharp/branch/vNext
 [vNext-nix-badge]: https://travis-ci.org/libgit2/libgit2sharp.svg?branch=vNext
 [vNext-nix]: https://travis-ci.org/libgit2/libgit2sharp/branches

 [coverity-project]: https://scan.coverity.com/projects/2088
 [coverity-badge]: https://scan.coverity.com/projects/2088/badge.svg

 [coveralls-project]: https://coveralls.io/r/libgit2/libgit2sharp?branch=vNext
 [coveralls-badge]: https://coveralls.io/repos/libgit2/libgit2sharp/badge.svg?branch=vNext

## Quick contributing guide

 - Fork and clone locally
 - Create a topic specific branch. Add some nice feature. Do not forget the tests ;-)
 - Send a Pull Request to spread the fun!

More thorough information available in the [wiki][wiki].

 [wiki]: https://github.com/libgit2/libgit2sharp/wiki

## Optimizing unit testing
LibGit2Sharp strives to have comprehensive and robust unit test suite to insure the quality of the software and to assist new contributors and users who can use the tests as sample to jump start development. There are over one-thousand unit-tests for LibGit2Sharp, this number will only grow as functionality is added.

You can do a few things to optimize running unit-tests on Windows:

1. Set the `LibGit2TestPath` environment variable to a path in your development environment.
  * If the unit-test framework cannot find the specified folder at runtime, it will fall back to the default location.
2. Configure your anti-virus software to ignore the `LibGit2TestPath` path.
3. Install a RAM disk like [IMDisk](http://www.ltr-data.se/opencode.html/#ImDisk) and set `LibGit2TestPath` to use it.
  * Use `imdisk.exe -a -s 256M -m X: -p "/fs:fat /q /v:ramdisk /y"` to create a RAM disk. This command requires elevated privileges and can be placed into a scheduled task or run manually before you begin unit-testing.

## Authors

 - **Code:** The LibGit2Sharp [contributors][committers]
 - **Logo:** [Jason "blackant" Long][blackant]

 [committers]: https://github.com/libgit2/libgit2sharp/contributors
 [blackant]: https://github.com/jasonlong

## License

The MIT license (Refer to the [LICENSE.md][license] file)

 [license]: https://github.com/libgit2/libgit2sharp/blob/master/LICENSE.md
