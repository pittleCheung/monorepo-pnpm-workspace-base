# 教程
https://blog.csdn.net/weixin_69230790/article/details/136389501


- 1. 在整个项目根目录下（monorepo-pnpm-workspace-base）安装依赖。
     所有工作空间安装依赖：在根目录下运行pnpm install命令，它会自动安装所有子项目的依赖。
    `pnpm i`

给某个子项目单独安装指定依赖
pnpm add axios --filter app2

- 安装workspace依赖

下边命令式packages下所有项目都安装，也可以指定项目安装如第一点
pnpm i @common/components -w

-w 或 --workspace: 这个标志告诉 pnpm 在当前 monorepo 的所有工作区（workspaces）中安装这个包。在 monorepos 中，你可能会有多个 npm 包位于同一个代码库的不同目录下，并使用 pnpm 的工作区功能来管理它们之间的依赖关系。使用 -w 标志可以确保 @common/components 被安装到所有需要它的工作区中。

如果在根目录下安装依赖的话，这个依赖可以在所有的packages中使用。如果需要为具体的一个package安装依赖，如何处理？

pnpm 提供了 --filter 参数。
指定项目按照common下依赖(app-base项目下安装 @common/components)
pnpm i @common/components --filter app-base
or
pnpm -F @packages/app-base install @common/components   (-F 就是--filter的别名)



# menorepo 统一管理版本的依赖 使用细则

启动项目
pnpm run dev
```js
1. 在 monorepo 根目录下运行以下命令来安装所有包的依赖：
pnpm install

2. 为特定项目安装依赖
// 给每个mono 安装具体的某个包 , 使用 -C 选项指定特定项目来安装依赖。
pnpm add vite@latest -C apps/deeplogic.monitor -D

```

> https://www.pnpm.cn/pnpm-workspace_yaml

`在整个项目根目录下`（monorepo-pnpm-workspace-base）安装依赖。

所有工作空间安装依赖：在根目录下运行pnpm install命令，它会自动安装所有子项目的依赖。
`pnpm i`

给某个子项目单独安装指定依赖
pnpm add axios --filter app2

- 安装workspace依赖  

下边命令是packages下所有项目都安装，也可以指定项目安装如第一点
pnpm i @deeplogic/materials -w

.npmrc文件下 指定ignore-workspace-root-check=true可以忽略-w 参数 默认下载到workspace-root中

-w 或 --workspace: 这个标志告诉 pnpm 在当前 monorepo 的所有工作区（workspaces）中安装这个包。在 monorepos 中，
你可能会有多个 npm 包位于同一个代码库的不同目录下，并使用 pnpm 的工作区功能来管理它们之间的依赖关系。
使用 -w 标志可以确保 @deeplogic.monitor 被安装到所有需要它的工作区中。

如果在根目录下安装依赖的话，这个依赖可以在所有的packages中使用。如果需要为具体的一个package安装依赖，如何处理？

pnpm 提供了 --filter 参数。
指定项目按照common下依赖(deeplogic.materials项目下安装 @deeplogic.monitor)
pnpm i axios --filter deeplogic.monitor   or   pnpm -F deeplogic.monitor install axios   (-F 就是--filter的别名)


文档参考
https://juejin.cn/post/7017817146314981413#comment


# 仓库管理 zustand

文档参考

> https://docs.pmnd.rs/zustand/getting-started/introduction

```js
export const useAppStore = createWithEqualityFn<AppType>(
  (...a) => ({
    ...useEditorStore(...a),
    ...useSitesStore(...a),
    // ...useOtherStore(...a),  在此处扩展仓库
    // ...
  }),
  shallow,
)
```
createWithEqualityFn 详见

> https://github.com/pmndrs/zustand/discussions/1937#discussioncomment-6675672