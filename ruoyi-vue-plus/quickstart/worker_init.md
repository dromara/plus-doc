# 工作流初始化（版本 >= 5.3.0）
- - -

## Warm-Flow 官方文档

更多用法与源码细节请参考官方文档：

https://warm-flow.dromara.org/

## 快速体验流程

### 1. 导入示例流程

找到项目 `script/leave` 目录。

![输入图片说明](https://foruda.gitee.com/images/1737528580662433426/278d3b8c_1766278.png "屏幕截图")

### 2. 上传流程定义

进入流程定义页面，使用“部署流程文件”上传 `leave` 目录下的 JSON 文件。

![输入图片说明](https://foruda.gitee.com/images/1737528975450787044/2b48929f_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1737528992596110640/881526bb_1766278.png "屏幕截图")

### 3. 查看已导入流程

![输入图片说明](https://foruda.gitee.com/images/1741684556837623157/cb8b3779_1766278.png "屏幕截图")

### 4. 发布并发起流程

发布流程后，新建请假申请并提交，可查看审批流转信息。

![输入图片说明](https://foruda.gitee.com/images/1737529198433551084/1e961d02_1766278.png "屏幕截图")

![输入图片说明](https://foruda.gitee.com/images/1737529293185669649/1c30194d_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1737529302856228733/052b6189_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1737529316625150163/f3ecf909_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1737529323678968166/c778330e_1766278.png "屏幕截图")

## 新建自己的流程

### 1. 新增或复制流程

在流程定义页点击“新增”，或对已发布流程先“复制流程”。

![输入图片说明](https://foruda.gitee.com/images/1737529632287955095/4604eace_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1737530721343551790/0d38ef60_1766278.png "屏幕截图")

![输入图片说明](https://foruda.gitee.com/images/1737529730534307974/78d82138_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1737529771075624407/b5df401d_1766278.png "屏幕截图")

### 2. 进入流程设计器

![输入图片说明](https://foruda.gitee.com/images/1737529842608265974/1779f073_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1737529929465786270/f1c3cacb_1766278.png "屏幕截图")

### 3. 编辑并保存流程

**注意：流程开始节点后必须跟随“申请人节点”。**  
该节点用于承载申请人相关事件（驳回、退回、草稿等），不需要填写具体办理人。

![输入图片说明](https://foruda.gitee.com/images/1737530221135678481/832e3b1e_1766278.png "屏幕截图")

### 4. 节点参数与表达式

设计器节点参数支持 SpEL 表达式，可调用 Bean 方法或使用变量占位符：

- `#{@deptService.getLeader()}`
- `${办理人变量}`

更多用法参考：
https://warm-flow.dromara.org/master/advanced/variableStategy.html

```java
// 简单案例参考 请按实际业务为准
// #{@deptService.getLeader()}
// #{@deptService.getLeader1(#handler1)}
@Service
// @Service("ssssss") // 重命名成自己喜欢的名字 方便书写查找 #{@ssssss.getLeader()}
public class DeptService {
    
    // 获取部门领导
    public String getLeader() {
        return "1";
    }

    // 获取其他流程变量当参数
    public String getLeader1(String handler1) {
        return "1";
    }
    
}
```

![输入图片说明](https://foruda.gitee.com/images/1737530283534208575/28bc3ce2_1766278.png "屏幕截图")

![输入图片说明](https://foruda.gitee.com/images/1737530405595713291/588d498f_1766278.png "屏幕截图")

### 5. 发布流程

保存后点击“发布流程”。

![输入图片说明](https://foruda.gitee.com/images/1737530463821262498/1b717351_1766278.png "屏幕截图")

点击 `发布流程` 发布修改完成的流程

![输入图片说明](https://foruda.gitee.com/images/1737530573466145192/cbbf3783_1766278.png "屏幕截图")

发布完成后 会跳转到 `已发布` 页面 流程版本号已经变成新的版本号了

![输入图片说明](https://foruda.gitee.com/images/1737530652110891393/3fc50c4b_1766278.png "屏幕截图")

## 开发接入要点

- 前端需编写业务表单与节点表单（可参考 `leaveEdit.vue`）
- 表单完成后在菜单管理中配置路由地址
- 框架目前仅支持自定义表单，动态表单能力有限

![输入图片说明](https://foruda.gitee.com/images/1752734965749669664/5e17d167_1766278.png "屏幕截图")

![输入图片说明](https://foruda.gitee.com/images/1752734994157820408/8aaf8da7_1766278.png "屏幕截图")

![输入图片说明](https://foruda.gitee.com/images/1752735194401620299/483d8be3_1766278.png "屏幕截图")

![输入图片说明](https://foruda.gitee.com/images/1752735101502377412/0dc57f2d_1766278.png "屏幕截图")

最后将写好的表单加入到菜单管理内 流程定义页面直接填表单的路由地址即可<br>

![输入图片说明](https://foruda.gitee.com/images/1752735483678305437/d7d6aa7f_1766278.png "屏幕截图")

## 后端监听器与 API

后端除业务 CRUD 外，需要实现三个监听器（参考 `TestLeaveServiceImpl`）。

![输入图片说明](https://foruda.gitee.com/images/1737531090579752181/b23c7411_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1752716138166254804/35e6a965_1766278.png "屏幕截图")
![输入图片说明](https://foruda.gitee.com/images/1737531104539008756/f1a43a7f_1766278.png "屏幕截图")

监听器说明：

- `processHandler`：流程状态监听（草稿、撤销、退回、作废、终止、完成等）
- `processTaskHandler`：任务创建监听（上一任务完成事件）
- `processDeleteHandler`：流程删除监听（同步清理业务数据）

事件注解示例：

`@EventListener(condition = "#processEvent.flowCode=='业务code'")`

### WorkflowService API

通用接口位于 `common-core` 模块的 `WorkflowService`，提供发起、审批、变量设置与查询等能力。  
用于业务模块与工作流模块交互，避免直接依赖工作流模块。

![输入图片说明](https://foruda.gitee.com/images/1737531677878180377/85899f22_1766278.png "屏幕截图")
