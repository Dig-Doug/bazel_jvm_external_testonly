Demonstrates an issue where a maven installed dep. references a test only target from gRPC.


```
bazel build @maven//:all
INFO: Invocation ID: 08954734-e403-4eec-9ca0-080547742415
ERROR: /home/doug/.cache/bazel/_bazel_doug/17380d495aa0e0d3997c90efd7604ee8/external/maven/BUILD:4311:11: in jvm_import rule @maven//:org_apache_beam_beam_sdks_java_io_google_cloud_platform: non-test target '@maven//:org_apache_beam_beam_sdks_java_io_google_cloud_platform' depends on testonly target '@io_grpc_grpc_java//testing:testing' and doesn't have testonly attribute set
ERROR: Analysis of target '@maven//:org_apache_beam_beam_sdks_java_io_google_cloud_platform_2_21_0' failed; build aborted: Analysis of target '@maven//:org_apache_beam_beam_sdks_java_io_google_cloud_platform' failed
INFO: Elapsed time: 0.155s
INFO: 0 processes.
FAILED: Build did NOT complete successfully (1 packages loaded, 2 targets configured)
```
