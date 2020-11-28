See [.gitlab-ci.yaml](./.gitlab-ci.yaml) for currently used docker images.

Non-template jobs prefixed with `.` are disabled because we only need to rebuild them when `r-release` got upgraded.
Branch building R-devel images is disabled by putting dummy echo command to `script`, so the child jobs can proceed without rebuilding parent.

