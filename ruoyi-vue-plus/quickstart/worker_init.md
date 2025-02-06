# 工作流初始化(版本 >= 5.3.0)
- - -

## Warm-Flow 官方文档

更多用法与源码细节请仔细观看官方文档 
工作流是个很复杂的东西不是几天就能理解的 请耐心学习

https://warm-flow.dromara.org/

### 工作流使用及配置方式

1.找到项目中`script`下`leave`文件夹

![输入图片说明](https://foruda.gitee.com/images/1737528580662433426/278d3b8c_1766278.png "屏幕截图")

2.启动项目找到流程定义通过`部署流程文件`将`leave`文件夹下JSON文件上传

![输入图片说明](https://foruda.gitee.com/images/1737528975450787044/2b48929f_1766278.png "屏幕截图")

![输入图片说明](https://foruda.gitee.com/images/1737528992596110640/881526bb_1766278.png "屏幕截图")

3.导入JSON文件后将会出现以下列表

![输入图片说明](https://foruda.gitee.com/images/1737529038122612127/39d6cb06_1766278.png "屏幕截图")


4.新增一条请假申请，提交后将会得到如下信息

![输入图片说明](https://foruda.gitee.com/images/1737529198433551084/1e961d02_1766278.png "屏幕截图")

提交之后点击查看流程可查看流程相关审批信息

![输入图片说明](https://foruda.gitee.com/images/1737529293185669649/1c30194d_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1737529302856228733/052b6189_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1737529316625150163/f3ecf909_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1737529323678968166/c778330e_1766278.png "屏幕截图")

### 如何新建自己的流程

1.点击`流程定义`页面`新增`按钮 这里我们查看已经写好的`leave1`点击`编辑`按钮

![输入图片说明](https://foruda.gitee.com/images/1737529632287955095/4604eace_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1737530721343551790/0d38ef60_1766278.png "屏幕截图")

2.新增流程后会跳转到`未发布`的流程页面 如果需要改动`已发布`的流程需要先`复制流程`

![输入图片说明](https://foruda.gitee.com/images/1737529730534307974/78d82138_1766278.png "屏幕截图")

3.复制完成后会跳转到`未发布`页面与`新增`逻辑一致

![输入图片说明](https://foruda.gitee.com/images/1737529771075624407/b5df401d_1766278.png "屏幕截图")

4.点击`流程设计`进入流程编辑器页面修改流程

![输入图片说明](https://foruda.gitee.com/images/1737529842608265974/1779f073_1766278.png "屏幕截图")

![输入图片说明](https://foruda.gitee.com/images/1737529929465786270/f1c3cacb_1766278.png "屏幕截图")

5.编辑修改流程内容并提交保存

![输入图片说明](https://foruda.gitee.com/images/1737530221135678481/832e3b1e_1766278.png "屏幕截图")

设计器节点参数均支持spel表达式 可使用表达式调用bean方法例如 `#{@deptService.getLeader()}` <br>
或者 `${办理人变量}` 书写办理人变量占位符 使用API工具动态注入办理人的id等用法 更多用法请参考warmflow官方文档<br>
https://warm-flow.dromara.org/master/advanced/variableStategy.html

```java
// 简单案例参考 请按实际业务为准
// #{@deptService.getLeader()}
@Service
// @Service("ssssss") // 重命名成自己喜欢的名字 方便书写查找 #{@ssssss.getLeader()}
public class DeptService {
    
    // 获取部门领导
    public String getLeader() {
        return "1";
    }
    
}
```

![输入图片说明](https://foruda.gitee.com/images/1737530283534208575/28bc3ce2_1766278.png "屏幕截图")

![输入图片说明](https://foruda.gitee.com/images/1737530405595713291/588d498f_1766278.png "屏幕截图")

6.修改流程完成后 点击设计器右上角`保存`按钮

![输入图片说明](https://foruda.gitee.com/images/1737530463821262498/1b717351_1766278.png "屏幕截图")

7.点击 `发布流程` 发布修改完成的流程

![输入图片说明](https://foruda.gitee.com/images/1737530573466145192/cbbf3783_1766278.png "屏幕截图")

发布完成后 会跳转到 `已发布` 页面 流程版本号已经变成新的版本号了

![输入图片说明](https://foruda.gitee.com/images/1737530652110891393/3fc50c4b_1766278.png "屏幕截图")

8.新流程需要编写代码的地方(重点!!!!)

> 前端需要编写业务的表单页面 与 各个节点的表单页面(不需要节点表单可以不写)<br>
> 具体书写方式参考 框架自带的 `leaveEdit.vue` 请假页面 根据业务逻辑修改表单内容即可<br>

![输入图片说明](https://foruda.gitee.com/images/1737530863662464931/15dabdd0_1766278.png "屏幕截图")

这里说明 框架目前只支持自定义编写表单使用 因为自定义编写业务表单可以最大程度的适配各种复杂的业务<br>
动态表单 适用于简单业务(warm-flow官方后续会增加此功能) 表单能力与数据交互能力均有限 目前不支持<br>

> 后端需要编写除业务代码的curd之外 针对工作流需要编写三个监听器<br>
> 参考自带请假流程 `TestLeaveServiceImpl` 实现类最下方三个监听器<br>


![输入图片说明](https://foruda.gitee.com/images/1737531090579752181/b23c7411_1766278.png "屏幕截图")

![输入图片说明](https://foruda.gitee.com/images/1737531098083304417/374ffd2d_1766278.png "屏幕截图")

![输入图片说明](https://foruda.gitee.com/images/1737531104539008756/f1a43a7f_1766278.png "屏幕截图")

`processHandler` 总体流程监听器(例如: 撤销，退回，作废，终止，已完成等) 用于更新业务与流程之间的一些数据和状态<br>
`processTaskHandler` 执行办理任务监听器 通常用于任务发起监听更新任务状态<br>
`processDeleteHandler` 流程删除监听器 用于监听流程被删除 同步删除业务数据<br>

书写方式参考demo写法即可 注解表达式为spel语法<br>
`@EventListener(condition = "#processEvent.flowCode=='业务code'")`<br>

9.后端API使用 查看 `common-core` 模块 通用接口 `WorkflowService`

![输入图片说明](https://foruda.gitee.com/images/1737531677878180377/85899f22_1766278.png "屏幕截图")

内部包含很多使用api 例如发起流程 审批流程 设置流程变量 获取流程变量等功能<br>
用于其他业务模块与工作流模块进行业务和数据交互 禁止其他业务模块导入工作流模块这种恶劣的使用方式!!<br>

