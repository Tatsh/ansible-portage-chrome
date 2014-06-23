# Required variables

* `gentoo_arch` A system Gentoo supports like `amd64`

# Variables

## `chrome_package`

Choose the Chrome version desired:

* `chromium`
* `google-chrome`
* `google-chrome-beta`
* `google-chrome-unstable`

Pick `google-chrome` if you want this to be 'fast'.

## `chrome_include_plugins`

Defaults to `true`. Whether or not to install the binary plugins.

## `chrome_stable_level`

Should be `null`, `''`, `~{{gentoo_arch}}`, or `**`.

## `chrome_version_type`

Choices are `stable`, `beta` and `unstable`. This should match with the `chrome_stable_level`. Example: if using `**` for `chrome_stable_level`, use `unstable` for this variable. This is only required if `chrome_include_plugins` is `true`.

## `chrome_use_flags`

List of USE flags for the build. Only applies if `chrome_package` is `chromium`.

## `chrome_no_splitdebug`

Defaults to `true`. This is to speed up compilation, the splitting of debug data (the `strip` command ran after compilation), and to reduce the amount of RAM required to build.

If this is `true`, then a configuration like the following is required:

```yaml
make_conf:
    cflags:
        - -O2
        - -pipe
        - -march=native
        - -fomit-frame-pointer
        - -ggdb  # Optional
    cxxflags:
        - '${CFLAGS}'
    features:
        - splitdebug  # Does not have to be set but this key must exist in make_conf
```
