# 开发规范
- - -

### 新增view
> 在`@/views`文件下创建对应的文件夹，一般性一个路由对应一个文件， 该模块下的功能就建议在本文件夹下创建一个新文件夹，各个功能模块维护自己的`utils`或`components`组件。

补充说明：

- 页面组件建议使用 `<script setup name="xxx">` 明确组件名，并与路由 `name` 保持一致，方便页签缓存、刷新和调试定位。
- 页面专属的 `components`、`utils`、`hooks` 尽量放在当前业务目录下，就近维护，避免全部堆到全局目录。
- 列表页建议统一保持 `queryParams`、`getList`、`handleQuery`、`resetQuery` 这类命名习惯，和现有页面及生成代码保持一致。

### 新增api
> 在`@/api`文件夹下创建本模块对应的api服务。  
> 在api服务同级创建`types.ts`类型声明文件。

补充说明：

- 推荐目录结构为 `@/api/模块/index.ts` + `types.ts`，接口定义与类型声明分离，后续维护成本更低。
- 页面中尽量直接引用 `VO`、`Query`、`Form` 等类型，避免长期使用 `any`。
- 请求默认会自动携带 `Authorization`、`clientid`、`Content-Language`，只有特殊场景再通过请求头显式控制 `isToken`、`repeatSubmit`、`isEncrypt`。

### 新增组件
> 在全局的`@/components`写一些全局的组件，如富文本，各种搜索组件，封装的分页组件等等能被公用的组件。 每个页面或者模块特定的业务组件则会写在当前`@/views`下面。
如：`@/views/system/user/components/xxx.vue`。这样拆分大大减轻了维护成本。

补充说明：

- `@/components` 更适合沉淀基础能力组件，和具体业务强耦合的组件建议保留在业务目录中。
- 项目已通过 `unplugin-vue-components` 对大量 Element Plus 组件做按需自动导入，但 `@/components` 下的自定义组件并不是全部全局可用，仍要按实际导入方式处理。

### 新增样式
> 页面的样式和组件是一个道理，全局的`@/style`放置一下全局公用的样式，每一个页面的样式就写在当前 views下面，请记住加上scoped 就只会作用在当前组件内了，避免造成全局的样式污染。

补充说明：

- 页面样式优先跟随页面文件维护，跨页面重复出现的变量、mixins、主题样式再抽到全局。
- `scoped` 只能解决大部分样式隔离问题，如果需要覆盖第三方组件深层结构，再局部使用 `:deep()`，不要直接放大为全局样式覆盖。
