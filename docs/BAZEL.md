# Building Angular with Bazel

> 用Bazel构建Angular

Note: this doc is for developing Angular, it is _not_ public
documentation for building an Angular application with Bazel.

> 请注意:这个是开发Angular的文档，不是一个使用Bazel来构建Angular应用的公共文档。

The Bazel build tool (http://bazel.build) provides fast, reliable
incremental builds. We plan to migrate Angular's build scripts to
Bazel.

> Bazel构建工具提供了一个快速的，可靠的增量构建方式，我们计划用Bazel迁移Angular的构建脚本。

## Installation

> 安装

Install Bazel from the distribution, see [install] instructions.
On Mac, just `brew install bazel`.

> 安装Bazel,请看 [install] 指令介绍，在Mac平台下，执行brew install bazel即可安装。

Bazel will install a hermetic version of Node, npm, and Yarn when
you run the first build.

> Bazel将会在你第一次build的时候安装一个由Node,npm,yarn组成的hermetic version（密封的版本？）。

[install]: https://bazel.build/versions/master/docs/install.html

## Configuration

> 配置

The `WORKSPACE` file indicates that our root directory is a
Bazel project. It contains the version of the Bazel rules we
use to execute build steps, from `build_bazel_rules_typescript`.
The sources on [GitHub] are published from Google's internal
repository (google3).

That repository defines dependencies on specific versions of
all the tools. You can run the tools Bazel installed, for
example rather than `yarn install` (which depends on whatever
version you have installed on your machine), you can
`bazel run @yarn//:yarn`.

Bazel accepts a lot of options. We check in some options in the
`.bazelrc` file. See the [bazelrc doc]. For example, if you don't
want Bazel to create several symlinks in your project directory
(`bazel-*`) you can add the line `build --symlink_prefix=/` to your
`.bazelrc` file.

[GitHub]: https://github.com/bazelbuild/rules_typescript
[bazelrc doc]: https://bazel.build/versions/master/docs/bazel-user-manual.html#bazelrc

## Building Angular

- Build a package: `bazel build packages/core`
- Build all packages: `bazel build packages/...`

You can use [ibazel] to get a "watch mode" that continuously
keeps the outputs up-to-date as you save sources. Note this is
new as of May 2017 and not very stable yet.

[ibazel]: https://github.com/bazelbuild/bazel-watcher
