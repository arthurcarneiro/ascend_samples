# Mindstudio运行图片样例
 
当前案例提供的操作指导都是基于命令行方式运行的，主要原因是命令行方式的兼容性更强。

这里提供如何在Mindstudio运行图片样例的通用指导，如有需要使用Mindstudio，可按照本指导操作并运行样例。

**注：本指导以Mindstudio安装在普通用户$HOME目录下为例说明**

## 环境要求

部署此sample前，需要准备好以下环境：

- 请确认已按照[环境准备和依赖安装](https://gitee.com/ascend/samples/tree/master/cplusplus/environment)准备好环境。

- 已完成对应产品的开发环境和运行环境安装。

- 环境中已经安装对应版本[Mindstudio](https://www.huaweicloud.com/ascend/resources/tools/mindstudio/download)。

## Mindstudio工程构建

1. 准备工程。

   按照对应样例下的命令行方式运行的README软件准备章节，准备好源码、模型、测试文件。

2. 非root用户命令行中执行以下命令，打开Mindstudio。

    **cd ~/MindStudio-ubuntu/bin**

    **./MindStudio.sh**

    ![](https://images.gitee.com/uploads/images/2020/1106/160652_6146f6a4_5395865.gif "icon-note.gif") **说明：**  
    > - 打开Mindstudio时如果有报错，请在普通用户下按照红色报错命令安装相关依赖后重新打开Mindstudio。

3. 构建Mindstudio工程。

    请检查想要使用Mindstudio运行的工程中是否包含\.project和\*.iml文件。  
    **如果包含，则可以直接使用Mindstudio打开工程，以googlenet_imagenet_picture为例说明。**   
    **如果不包含，需要构建Mindstudio工程，以colorization_picture为例说明。**

    - 直接使用Mindstudio打开工程。   
       - 首次登录MindStudio：单击**Open or Import**，然后选择对应工程，如googlenet_imagenet_picture。   
       - 非首次登录MindStudio：在顶部菜单栏中选择**File \> Open**，然后选择对应工程，如googlenet_imagenet_picture。
        
    - 构建Mindstudio工程。   
        1. 进入工程创建页面。   
            - 首次登录MindStudio：单击**Create New Project**。   
            - 非首次登录MindStudio：在顶部菜单栏中选择**File \> New \> Project\.\.\.**。
    
        2. 在**New Project**窗口中，选择**Ascend App**，填写工程名称，例如**colorization_picture**。然后点击**Next**。
    
        3. 在**New Project**窗口中，选择工程类型为**Empty Project**，创建一个仅包括开发框架的工程，不含具体的代码逻辑。单击**Finish**，完成工程创建。

        4. 命令行中执行以下命令，将samples源码复制到Mindstudio空工程中。

            **cp -r ~/samples/c++/level2_simple_inference/6_other/colorization_picture/\* ~/AscendProject/colorization_picture**

        5. 在Mindstudio中右击工程，选择**Reload from Disk**刷新工程即可。

### 样例编译。
    
在Mindstudio右上角点击 Build->Edit Build Configuration... ,进行编译配置。

- 使用产品为200DK开发者板，选择 Target Architecture为aarch64。

- 使用产品为300加速卡（ai1s云端推理环境），选择 Target Architecture为x86_64。

选择完成后点击Build开始编译,编译完成后，会在工程中生成build和out文件夹。

### 样例运行

1. 在Mindstudio右上角点击 **Run->Edit Configurations...** ,进行运行配置。   

   **Target Host Ip** 选择为已经配置好的运行环境ip地址。一般USB方式连接的200DK为192.168.1.2，ai1s云端推理环境为公网ip地址。   

   **Command Arguments** 填写为：**../data**。

   参数填写完成后，点击右下角的**Apply**，再点击**OK**。
​    
    ![](https://images.gitee.com/uploads/images/2020/1106/160652_6146f6a4_5395865.gif "icon-note.gif") **说明：**  
    > - 如果**Target Host Ip**没有取值，请点击后面的加号图标，自行配置运行环境。   

2. 在Mindstudio右上角点击 **Run->Run 'XXX'** ,运行样例。

    运行过程中，会将开发环境中的**data、out、model**文件夹上传到运行环境。并使用**adc**工具执行编译出来的**run.sh**脚本。

    ![](https://images.gitee.com/uploads/images/2020/1106/160652_6146f6a4_5395865.gif "icon-note.gif") **说明：**  
    > - **XXX**指对应Mindstudio工程。 
    >- 如果运行有so找不到的报错，请参考[如何重启ada进程](https://support.huaweicloud.com/ug-mindstudioc75/atlasms_02_0224.html)说明，在运行环境重启ada。

3. 查看结果。

    运行完成后，会在Mindstudio中打印输出，部分样例会在Mindstudio的out目录下回传推理处理后的图片。
