# S-TaLiRo Dockerfile

This Dockerfile is used to build S-TaLiRo with the following components:

- [DP-TaLiRo](https://cpslab.assembla.com/spaces/s-taliro_public/subversion/source/HEAD/trunk/dp_taliro)
- [TP-TaLiRo](https://cpslab.assembla.com/spaces/s-taliro_public/subversion/source/HEAD/trunk/tp_taliro)

Please note, a license is required to build the image. When building, ensure you set the `--build-arg LICENSE` to the path to your Mathworks downloaded license on your host machine for it to be copied properly.

In addition, there is a pushed version of this image without a license. Therefore, you must perform one of the following to use MATLAB:

1. Copy the `license.lic` (can be downloaded from Mathworks) into the following path: `/opt/matlab/licenses/` on the Docker container, or...
2. Set `MLM_LICENSE_FILE` to your Mathworks server license or to a different directory on the Docker container of your copied license file if you did Step 1.
