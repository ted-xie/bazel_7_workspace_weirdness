# Weird WORKSPACE sequential declaration issue

## Synopsis

A WORKSPACE file is loaded sequentially by Bazel. In other words, if a WORKSPACE file contains _multiple_ sequential loads of the same dependency twice, i.e.:

```python
http_archive(
    name = "my_thing",
    urls = ["A.zip"],
)

http_archive(
    name = "my_thing",
    urls = ["B.zip"],
)
```

Then the B.zip version should "win" and be the final `@my_thing` dependency visible to the user.

This repository seems to indicate that the opposite is true. In this repo's WORKSPACE file, I have copy-pasted the WORKSPACE stanzas for rules_java versions 7.12.2 and 8.5.1, which are backwards-incompatible. Specifically, the setup stanza for rules_java 8.5.1 references files (specifically `@rules_java//java:rules_java_deps.bzl`) that do not exist in the earlier 7.12.2 version. See https://github.com/bazelbuild/rules_java/tree/7.12.2/java.

If the sequential ordering property of WORKSPACE files worked properly, then the v8.5.1 setup stanza should work flawlessly. However, it currently fails, complaining about a missing file:

```shell
$ bazelisk query @rules_java//...
ERROR: Error computing the main repository mapping: cannot load '@@rules_java//java:rules_java_deps.bzl': no such file
```

This failure seems to indicate that the rules_java dep is not properly overwritten in the second http_archive() declaration.

## Misc info
* Bazel version: 7.4.1
* Repro instructions: `./repro.sh`

