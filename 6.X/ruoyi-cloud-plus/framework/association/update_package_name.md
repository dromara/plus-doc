# 关于修改包名
- - -

## 前置说明

- 由于 dromara 依赖较多，IDEA 可能无法一次性识别完整包名

## 操作步骤

### 1. 新建包用于重命名

先新建 `org.dromara` 包。

![输入图片说明](https://foruda.gitee.com/images/1708491220807198688/b95c0c34_1766278.png "屏幕截图")

### 2. 使用 IDEA 重构重命名

在包上右键 `Refactor -> Rename`，选择 `All Directories`。

![输入图片说明](https://foruda.gitee.com/images/1683276891079076405/79808b22_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1708491697128844860/1e87ad39_1766278.png "屏幕截图")

如果 IDEA 无法识别完整包名，可先将 `dromara` 改为临时包名（如 `ruoyi`），再重复上述步骤。

![输入图片说明](https://foruda.gitee.com/images/1708490576909691001/692e5b37_1766278.png "屏幕截图")

**需要先将dromara修改为 例如: ruoyi 然后重复上述步骤 这样就可以整包修改了**
<br>
![输入图片说明](https://foruda.gitee.com/images/1708490906933084793/ff104cd7_1766278.png "屏幕截图")

### 3. 全局替换包名

使用 IDEA 全局替换：`org.dromara` -> `com.xxx`。

![输入图片说明](https://foruda.gitee.com/images/1708491055347995519/dedda0d1_1766278.png "屏幕截图")

**注意：不要替换第三方依赖包名，例如 `org.dromara.sms4j`。**

### 4. 检查 SPI 文件

完成后检查所有 `common` 模块下的 SPI 文件是否正确。

![输入图片说明](https://foruda.gitee.com/images/1708491365841192006/8bc337c2_1766278.png "屏幕截图")
