# Generic Android Kernel CI (Kleaf / Bazel)

A customizable GitHub Actions workflow designed for building Android Kernels using Google's **Kleaf / Bazel** build system. It automatically syncs kernel source manifests, executes Bazel targets with flexible build configs, packages the distribution binaries, and publishes output artifacts.

---

## Workflow Inputs

When triggering the workflow manually via **`workflow_dispatch`**, you can configure the following build parameters:

* **`MANIFEST_URL`**: The Git repository URL of the kernel manifest (Default: `https://android.googlesource.com/kernel/manifest`).
* **`MANIFEST_BRANCH`**: The target manifest branch to sync (Default: `common-android-mainline`).
* **`BUILD_CONFIG`**: Additional Bazel configuration flags passed to the build command. Enter flags without the `--` prefix, separated by spaces (e.g., `nosandbox_debug config=fast` will automatically expand to `--nosandbox_debug --config=fast`).
* **`BUILD_PATH`**: The Bazel package or path relative to the workspace (Default: `common`).
* **`BUILD_TARGET`**: The target rule name to execute (Default: `kernel_aarch64_dist`). Together with `BUILD_PATH`, it constructs the target `//<BUILD_PATH>:<BUILD_TARGET>` (e.g., `//common:kernel_aarch64_dist`).
* **`PUBLISH_TYPE`**: Selection strategy for publishing output build artifacts:
  * `release`: Uploads artifacts as a new GitHub Release.
  * `artifact`: Stores artifacts in GitHub Actions Artifacts.
  * `both`: Publishes to both GitHub Releases and Actions Artifacts.

---

## Output Naming Schema

Generated release tags and artifact packages strictly follow this naming convention:

`${DATE}-${MANIFEST_BRANCH}-${BUILD_TARGET}-${COMMIT_SHA}`

**Example Tag**: `2026.08.26-common-android-mainline-kernel_aarch64_dist-a1b2c3d4`

---

## License

This project is licensed under the Apache License 2.0 - see the [LICENSE](LICENSE) file for details.
