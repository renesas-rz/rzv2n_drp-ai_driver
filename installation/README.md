# Installation

RZ/V2N DRP-AI Driver can be added even after RZ/V2N Linux build environment is built.  
Please follow the steps below to add the RZ/V2N DRP-AI Driver to your RZ/V2N Linux build environment. 

#### 1. Store the downloaded RZ/V2N DRP-AI Driver (eg rzv2n_drp-ai_driver_ver.x.xx.tar.gz) in the $WORK* directory.   
*: $WORK is the Linux build directory.  

#### 2. Use the following command to deploy the DRP-AI Driver in the RZ/V2N Linux environment.
~~~  
$ tar xvf rzv2n_drp-ai_driver_ver.x.xx.tar.gz  
$ mkdir -p meta-rz-features
$ mv rzv2n_drp-ai_driver_ver.x.xx/meta-rz-features/meta-rz-drpai/ ./meta-rz-features/
$ TEMPLATECONF=${PWD}/meta-renesas/meta-rzv2n/docs/template/conf/ \
    source poky/oe-init-build-env
$ bitbake-layers add-layer ../meta-rz-features/meta-rz-drpai
~~~

#### 3. Rebuild the SD image with the following command.
~~~
$ MACHINE=rzv2n-evk bitbake linux-renesas -c compile -f
$ MACHINE=rzv2n-evk bitbake linux-renesas -c deploy
$ MACHINE=rzv2n-evk bitbake core-image-weston -c cleanall  
$ MACHINE=rzv2n-evk bitbake core-image-weston  
~~~  
When the rebuild is successfully completed, the following file is generated.  
$WORK/build/tmp/deploy/images/rzv2n-evk  

|File name|Explanation|
|:---|:---|
|Flash_Writer_SCIF_RZV2N_DEV_LPDDR4X.mot|Flash Writer|
|bl2_bp_spi-rzv2n-evk.srec|BL2 for xSPI boot|
|fip-rzv2n-evk.srec|FIP|
|core-image-weston-rzv2n-evk.wic.bmap|bmap file|
|core-image-weston-rzv2n-evk.wic.gz|WIC file|

#### 4. Generate the Cross Compiler with the following command.  
~~~  
$ MACHINE=rzv2n-evk bitbake core-image-weston -c populate_sdk  
~~~  
When the above command is successfully completed, the following is generated.  
$WORK/build/tmp/deploy/sdk  
* poky-glibc-x86_64-core-image-weston-aarch64-rzv2n-evk-toolchain-3.1.31.sh  

