# tsconfig

## 例子

```js
{
  "compilerOptions": {
    "target": "es5",
    "downlevelIteration": true,
    "module": "esnext",
    "strict": true,
    "jsx": "preserve",
    "importHelpers": true,
    "moduleResolution": "node",
    "experimentalDecorators": true,
    "esModuleInterop": true,
    "allowSyntheticDefaultImports": true,
    "sourceMap": true,
    "noImplicitAny": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "baseUrl": ".",
    "types": ["webpack-env"],
    "paths": {
      "@/*": ["src/*"]
    },
    "lib": ["esnext", "dom", "dom.iterable", "scripthost"]
  },
  "include": [
    "src/**/*.ts",
    "src/**/*.tsx",
    "src/**/*.vue",
    "tests/**/*.ts",
    "tests/**/*.tsx",
    "src/main.ts"
  ],
  "exclude": ["node_modules", "src/**/*.js"]
}

```

## 各个项目模板

### 基本的 TSConfig

根据你要在其中运行代码的不同的 JavaScript 运行时环境，你可以在 [github.com/tsconfig/bases](https://github.com/tsconfig/bases/) 上寻找一个合适的基本配置。 你可以通过扩展这些已经处理过不同的 JavaScript 运行时环境的 `tsconfig.json` 文件来简化你项目中的 `tsconfig.json`。

## 编译选项

| 选项                                 | 类型       | 默认值                                                       | 描述                                                         |
| :----------------------------------- | :--------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| `--allowJs`                          | `boolean`  | `false`                                                      | 允许编译javascript文件。                                     |
| `--allowSyntheticDefaultImports`     | `boolean`  | `module === "system"` 或设置了 `--esModuleInterop` 且 `module` 不为 `es2015` / `esnext` | 允许从没有设置默认导出的模块中默认导入。这并不影响代码的输出，仅为了类型检查。 |
| `--allowUnreachableCode`             | `boolean`  | `false`                                                      | 不报告执行不到的代码错误。                                   |
| `--allowUnusedLabels`                | `boolean`  | `false`                                                      | 不报告未使用的标签错误。                                     |
| `--alwaysStrict`                     | `boolean`  | `false`                                                      | 以严格模式解析并为每个源文件生成 `"use strict"`语句          |
| `--baseUrl`                          | `string`   |                                                              | 解析非相对模块名的基准目录。查看 [模块解析文档](https://www.tslang.cn/docs/handbook/module-resolution.html#base-url)了解详情。 |
| `--charset`                          | `string`   | `"utf8"`                                                     | 输入文件的字符集。                                           |
| `--checkJs`                          | `boolean`  | `false`                                                      | 在 `.js`文件中报告错误。与 `--allowJs`配合使用。             |
| `--declaration` `-d`                 | `boolean`  | `false`                                                      | 生成相应的 `.d.ts`文件。                                     |
| `--declarationDir`                   | `string`   |                                                              | 生成声明文件的输出路径。                                     |
| `--diagnostics`                      | `boolean`  | `false`                                                      | 显示诊断信息。                                               |
| `--disableSizeLimit`                 | `boolean`  | `false`                                                      | 禁用JavaScript工程体积大小的限制                             |
| `--emitBOM`                          | `boolean`  | `false`                                                      | 在输出文件的开头加入BOM头（UTF-8 Byte Order Mark）。         |
| `--emitDecoratorMetadata` [1]        | `boolean`  | `false`                                                      | 给源码里的装饰器声明加上设计类型元数据。查看 [issue #2577](https://github.com/Microsoft/TypeScript/issues/2577)了解更多信息。 |
| `--experimentalDecorators` [1]       | `boolean`  | `false`                                                      | 启用实验性的ES装饰器。                                       |
| `--extendedDiagnostics`              | `boolean`  | `false`                                                      | 显示详细的诊段信息。                                         |
| `--forceConsistentCasingInFileNames` | `boolean`  | `false`                                                      | 禁止对同一个文件的不一致的引用。                             |
| `--help` `-h`                        |            |                                                              | 打印帮助信息。                                               |
| `--importHelpers`                    | `string`   |                                                              | 从 [`tslib` ](https://www.npmjs.com/package/tslib)导入辅助工具函数（比如 `__extends`， `__rest`等） |
| `--inlineSourceMap`                  | `boolean`  | `false`                                                      | 生成单个sourcemaps文件，而不是将每sourcemaps生成不同的文件。 |
| `--inlineSources`                    | `boolean`  | `false`                                                      | 将代码与sourcemaps生成到一个文件中，要求同时设置了 `--inlineSourceMap`或 `--sourceMap`属性。 |
| `--init`                             |            |                                                              | 初始化TypeScript项目并创建一个 `tsconfig.json`文件。         |
| `--isolatedModules`                  | `boolean`  | `false`                                                      | 将每个文件作为单独的模块（与“ts.transpileModule”类似）。     |
| `--jsx`                              | `string`   | `"Preserve"`                                                 | 在 `.tsx`文件里支持JSX： `"React"`或 `"Preserve"`。查看 [JSX](https://www.tslang.cn/docs/handbook/jsx.html)。 |
| `--jsxFactory`                       | `string`   | `"React.createElement"`                                      | 指定生成目标为react JSX时，使用的JSX工厂函数，比如 `React.createElement`或 `h`。 |
| `--lib`                              | `string[]` |                                                              | 编译过程中需要引入的库文件的列表。 可能的值为： ► `ES5` ► `ES6` ► `ES2015` ► `ES7` ► `ES2016` ► `ES2017` ► `ES2018` ► `ESNext` ► `DOM` ► `DOM.Iterable` ► `WebWorker` ► `ScriptHost` ► `ES2015.Core` ► `ES2015.Collection` ► `ES2015.Generator` ► `ES2015.Iterable` ► `ES2015.Promise` ► `ES2015.Proxy` ► `ES2015.Reflect` ► `ES2015.Symbol` ► `ES2015.Symbol.WellKnown` ► `ES2016.Array.Include` ► `ES2017.object` ► `ES2017.Intl` ► `ES2017.SharedMemory` ► `ES2017.String` ► `ES2017.TypedArrays` ► `ES2018.Intl` ► `ES2018.Promise` ► `ES2018.RegExp` ► `ESNext.AsyncIterable` ► `ESNext.Array` ► `ESNext.Intl` ► `ESNext.Symbol`  注意：如果`--lib`没有指定默认注入的库的列表。默认注入的库为： ► 针对于`--target ES5`：`DOM，ES5，ScriptHost` ► 针对于`--target ES6`：`DOM，ES6，DOM.Iterable，ScriptHost` |
| `--listEmittedFiles`                 | `boolean`  | `false`                                                      | 打印出编译后生成文件的名字。                                 |
| `--listFiles`                        | `boolean`  | `false`                                                      | 编译过程中打印文件名。                                       |
| `--locale`                           | `string`   | *(platform specific)*                                        | 显示错误信息时使用的语言，比如：en-us。                      |
| `--mapRoot`                          | `string`   |                                                              | 为调试器指定指定sourcemap文件的路径，而不是使用生成时的路径。当 `.map`文件是在运行时指定的，并不同于 `js`文件的地址时使用这个标记。指定的路径会嵌入到 `sourceMap`里告诉调试器到哪里去找它们。 |
| `--maxNodeModuleJsDepth`             | `number`   | `0`                                                          | node_modules依赖的最大搜索深度并加载JavaScript文件。仅适用于 `--allowJs`。 |
| `--module` `-m`                      | `string`   | `target === "ES6" ? "ES6" : "commonjs"`                      | 指定生成哪个模块系统代码： `"None"`， `"CommonJS"`， `"AMD"`， `"System"`， `"UMD"`， `"ES6"`或 `"ES2015"`。 ► 只有 `"AMD"`和 `"System"`能和 `--outFile`一起使用。 ► `"ES6"`和 `"ES2015"`可使用在目标输出为 `"ES5"`或更低的情况下。 |
| `--moduleResolution`                 | `string`   | `module === "AMD" or "System" or "ES6" ? "Classic" : "Node"` | 决定如何处理模块。或者是`"Node"`对于Node.js/io.js，或者是`"Classic"`（默认）。查看[模块解析](https://www.tslang.cn/docs/handbook/module-resolution.html)了解详情。 |
| `--newLine`                          | `string`   | *(platform specific)*                                        | 当生成文件时指定行结束符： `"crlf"`（windows）或 `"lf"`（unix）。 |
| `--noEmit`                           | `boolean`  | `false`                                                      | 不生成输出文件。                                             |
| `--noEmitHelpers`                    | `boolean`  | `false`                                                      | 不在输出文件中生成用户自定义的帮助函数代码，如 `__extends`。 |
| `--noEmitOnError`                    | `boolean`  | `false`                                                      | 报错时不生成输出文件。                                       |
| `--noErrorTruncation`                | `boolean`  | `false`                                                      | 不截短错误消息。                                             |
| `--noFallthroughCasesInSwitch`       | `boolean`  | `false`                                                      | 报告switch语句的fallthrough错误。（即，不允许switch的case语句贯穿） |
| `--noImplicitAny`                    | `boolean`  | `false`                                                      | 在表达式和声明上有隐含的 `any`类型时报错。                   |
| `--noImplicitReturns`                | `boolean`  | `false`                                                      | 不是函数的所有返回路径都有返回值时报错。                     |
| `--noImplicitThis`                   | `boolean`  | `false`                                                      | 当 `this`表达式的值为 `any`类型的时候，生成一个错误。        |
| `--noImplicitUseStrict`              | `boolean`  | `false`                                                      | 模块输出中不包含 `"use strict"`指令。                        |
| `--noLib`                            | `boolean`  | `false`                                                      | 不包含默认的库文件（ `lib.d.ts`）。                          |
| `--noResolve`                        | `boolean`  | `false`                                                      | 不把 `/// <reference``>`或模块导入的文件加到编译文件列表。   |
| `--noStrictGenericChecks`            | `boolean`  | `false`                                                      | 禁用在函数类型里对泛型签名进行严格检查。                     |
| `--noUnusedLocals`                   | `boolean`  | `false`                                                      | 若有未使用的局部变量则抛错。                                 |
| `--noUnusedParameters`               | `boolean`  | `false`                                                      | 若有未使用的参数则抛错。                                     |
| `--out`                              | `string`   |                                                              | 弃用。使用 `--outFile` 代替。                                |
| `--outDir`                           | `string`   |                                                              | 重定向输出目录。                                             |
| `--outFile`                          | `string`   |                                                              | 将输出文件合并为一个文件。合并的顺序是根据传入编译器的文件顺序和 `///<reference``>`和 `import`的文件顺序决定的。查看输出文件顺序文件了解详情。 |
| `paths` [2]                          | `Object`   |                                                              | 模块名到基于 `baseUrl`的路径映射的列表。查看 [模块解析文档](https://www.tslang.cn/docs/handbook/module-resolution.html#path-mapping)了解详情。 |
| `--preserveConstEnums`               | `boolean`  | `false`                                                      | 保留 `const`和 `enum`声明。查看 [const enums documentation](https://github.com/Microsoft/TypeScript/blob/master/doc/spec.md#94-constant-enum-declarations)了解详情。 |
| `--preserveSymlinks`                 | `boolean`  | `false`                                                      | 不把符号链接解析为其真实路径；将符号链接文件视为真正的文件。 |
| `--preserveWatchOutput`              | `boolean`  | `false`                                                      | 保留watch模式下过时的控制台输出。                            |
| `--pretty` [1]                       | `boolean`  | `false`                                                      | 给错误和消息设置样式，使用颜色和上下文。                     |
| `--project` `-p`                     | `string`   |                                                              | 编译指定目录下的项目。这个目录应该包含一个 `tsconfig.json`文件来管理编译。查看 [tsconfig.json](https://www.tslang.cn/docs/handbook/tsconfig-json.html)文档了解更多信息。 |
| `--reactNamespace`                   | `string`   | `"React"`                                                    | 当目标为生成 `"react"` JSX时，指定 `createElement`和 `__spread`的调用对象 |
| `--removeComments`                   | `boolean`  | `false`                                                      | 删除所有注释，除了以 `/!*`开头的版权信息。                   |
| `--rootDir`                          | `string`   | *(common root directory is computed from the list of input files)* | 仅用来控制输出的目录结构 `--outDir`。                        |
| `rootDirs` [2]                       | `string[]` |                                                              | *根（root）*文件夹列表，表示运行时组合工程结构的内容。查看 [模块解析文档](https://www.tslang.cn/docs/handbook/module-resolution.html#virtual-directories-with-rootdirs)了解详情。 |
| `--skipDefaultLibCheck`              | `boolean`  | `false`                                                      | 忽略 [库的默认声明文件](https://www.tslang.cn/docs/handbook/triple-slash-directives.html#-reference-no-default-libtrue)的类型检查。 |
| `--skipLibCheck`                     | `boolean`  | `false`                                                      | 忽略所有的声明文件（ `*.d.ts`）的类型检查。                  |
| `--sourceMap`                        | `boolean`  | `false`                                                      | 生成相应的 `.map`文件。                                      |
| `--sourceRoot`                       | `string`   |                                                              | 指定TypeScript源文件的路径，以便调试器定位。当TypeScript文件的位置是在运行时指定时使用此标记。路径信息会被加到 `sourceMap`里。 |
| `--strict`                           | `boolean`  | `false`                                                      | 启用所有严格类型检查选项。 启用 `--strict`相当于启用 `--noImplicitAny`, `--noImplicitThis`, `--alwaysStrict`， `--strictNullChecks`和 `--strictFunctionTypes`和`--strictPropertyInitialization`。 |
| `--strictFunctionTypes`              | `boolean`  | `false`                                                      | 禁用函数参数双向协变检查。                                   |
| `--strictPropertyInitialization`     | `boolean`  | `false`                                                      | 确保类的非`undefined`属性已经在构造函数里初始化。若要令此选项生效，需要同时启用`--strictNullChecks`。 |
| `--strictNullChecks`                 | `boolean`  | `false`                                                      | 在严格的 `null`检查模式下， `null`和 `undefined`值不包含在任何类型里，只允许用它们自己和 `any`来赋值（有个例外， `undefined`可以赋值到 `void`）。 |
| `--stripInternal` [1]                | `boolean`  | `false`                                                      | 不对具有 `/** @internal */` JSDoc注解的代码生成代码。        |
| `--suppressExcessPropertyErrors` [1] | `boolean`  | `false`                                                      | 阻止对对象字面量的额外属性检查。                             |
| `--suppressImplicitAnyIndexErrors`   | `boolean`  | `false`                                                      | 阻止 `--noImplicitAny`对缺少索引签名的索引对象报错。查看 [issue #1232](https://github.com/Microsoft/TypeScript/issues/1232#issuecomment-64510362)了解详情。 |
| `--target` `-t`                      | `string`   | `"ES3"`                                                      | 指定ECMAScript目标版本 `"ES3"`（默认）， `"ES5"`， `"ES6"`/ `"ES2015"`， `"ES2016"`， `"ES2017"`或 `"ESNext"`。  注意： `"ESNext"`最新的生成目标列表为 [ES proposed features](https://github.com/tc39/proposals) |
| `--traceResolution`                  | `boolean`  | `false`                                                      | 生成模块解析日志信息                                         |
| `--types`                            | `string[]` |                                                              | 要包含的类型声明文件名列表。查看 [@types，--typeRoots和--types](https://www.tslang.cn/docs/handbook/tsconfig-json.html#types-typeroots-and-types)章节了解详细信息。 |
| `--typeRoots`                        | `string[]` |                                                              | 要包含的类型声明文件路径列表。查看 [@types，--typeRoots和--types](https://www.tslang.cn/docs/handbook/tsconfig-json.html#types-typeroots-and-types)章节了解详细信息。 |
| `--version` `-v`                     |            |                                                              | 打印编译器版本号。                                           |
| `--watch` `-w`                       |            |                                                              | 在监视模式下运行编译器。会监视输出文件，在它们改变时重新编译。监视文件和目录的具体实现可以通过环境变量进行配置。详情请看[配置 Watch](https://www.tslang.cn/docs/handbook/configuring-watch.html)。 |

## 概览

当目录中出现了 文件，则说明该目录是 TypeScript 项目的根目录。 文件指定了编译项目所需的根目录下的文件以及编译选项。`tsconfig.json``tsconfig.json`

JavaScript 项目可以使用 文件，它的作用与 基本相同，只是默认启用了一些 JavaScript 相关的编译选项。`jsconfig.json``tsconfig.json`

一个项目将以下列之一的方式编译：使用 或者`tsconfig.json` `jsconfig.json`

- 在调用 tsc 命令并且没有其它输入文件参数时，编译器将由当前目录开始向父级目录寻找包含 tsconfig 文件的目录。
- 调用 tsc 命令并且没有其他输入文件参数，可以使用 （或者只是 ）的命令行选项来指定包含了 的目录，或者包含有效配置的 文件路径。`--project``-p``tsconfig.json``.json`

当命令行中指定了输入文件参数， 文件会被忽略。`tsconfig.json`

**示例**

tsconfig.json示例文件:

- 使用"files"属性

```json
     {
    "compilerOptions": {
        "module": "commonjs",
        "noImplicitAny": true,
        "removeComments": true,
        "preserveConstEnums": true,
        "sourceMap": true
    },
    "files": [
        "core.ts",
        "sys.ts",
        "types.ts",
        "scanner.ts",
        "parser.ts",
        "utilities.ts",
        "binder.ts",
        "checker.ts",
        "emitter.ts",
        "program.ts",
        "commandLineParser.ts",
        "tsc.ts",
        "diagnosticInformationMap.generated.ts"
    ]
}     
```

使用`"include"`和`"exclude"`属性

```json
{
    "compilerOptions": {
        "module": "system",
        "noImplicitAny": true,
        "removeComments": true,
        "preserveConstEnums": true,
        "outFile": "../../built/local/tsc.js",
        "sourceMap": true
    },
    "include": [
        "src/**/*"
    ],
    "exclude": [
        "node_modules",
        "**/*.spec.ts"
    ]
}
```



**细节**

"compilerOptions"可以被忽略，这时编译器会使用默认值。在这里查看完整的[编译器选项](https://www.tslang.cn/docs/handbook/compiler-options.html)列表。

"files"指定一个包含相对或绝对文件路径的列表。 "include"和"exclude"属性指定一个文件glob匹配模式列表。 支持的glob通配符有：

- \* 匹配0或多个字符（不包括目录分隔符）
- ?  匹配一个任意字符（不包括目录分隔符）
- **/ 递归匹配任意子目录

如果一个glob模式里的某部分只包含`*`或`.*`，那么仅有支持的文件扩展名类型被包含在内（比如默认`.ts`，`.tsx`，和`.d.ts`， 如果 `allowJs`设置能`true`还包含`.js`和`.jsx`）。

如果`"files"`和`"include"`都没有被指定，编译器默认包含当前目录和子目录下所有的TypeScript文件（`.ts`, `.d.ts` 和 `.tsx`），排除在`"exclude"`里指定的文件。JS文件（`.js`和`.jsx`）也被包含进来如果`allowJs`被设置成`true`。 如果指定了 `"files"`或`"include"`，编译器会将它们结合一并包含进来。 使用 `"outDir"`指定的目录下的文件永远会被编译器排除，除非你明确地使用`"files"`将其包含进来（这时就算用`exclude`指定也没用）。

使用`"include"`引入的文件可以使用`"exclude"`属性过滤。 然而，通过 `"files"`属性明确指定的文件却总是会被包含在内，不管`"exclude"`如何设置。 如果没有特殊指定， `"exclude"`默认情况下会排除`node_modules`，`bower_components`，`jspm_packages`和`<outDir>`目录。

任何被`"files"`或`"include"`指定的文件所引用的文件也会被包含进来。 `A.ts`引用了`B.ts`，因此`B.ts`不能被排除，除非引用它的`A.ts`在`"exclude"`列表中。

需要注意编译器不会去引入那些可能做为输出的文件；比如，假设我们包含了`index.ts`，那么`index.d.ts`和`index.js`会被排除在外。 通常来讲，不推荐只有扩展名的不同来区分同目录下的文件。

`tsconfig.json`文件可以是个空文件，那么所有默认的文件（如上面所述）都会以默认配置选项编译。

在命令行上指定的编译选项会覆盖在`tsconfig.json`文件里的相应选项。

`@types`，`typeRoots`和`types`

默认所有*可见的*"`@types`"包会在编译过程中被包含进来。 `node_modules/@types`文件夹下以及它们子文件夹下的所有包都是*可见的*； 也就是说， `./node_modules/@types/`，`../node_modules/@types/`和`../../node_modules/@types/`等等。

如果指定了`typeRoots`，*只有*`typeRoots`下面的包才会被包含进来。 比如：

```json
{
   "compilerOptions": {
       "typeRoots" : ["./typings"]
   }
}
```

这个配置文件会包含*所有*`./typings`下面的包，而不包含`./node_modules/@types`里面的包。

如果指定了`types`，只有被列出来的包才会被包含进来。 比如：

```json
{
   "compilerOptions": {
        "types" : ["node", "lodash", "express"]
   }
}
```

### 使用`extends`继承配置



`tsconfig.json`文件可以利用`extends`属性从另一个配置文件里继承配置。

`extends`是`tsconfig.json`文件里的顶级属性（与`compilerOptions`，`files`，`include`，和`exclude`一样）。 `extends`的值是一个字符串，包含指向另一个要继承文件的路径。

在原文件里的配置先被加载，然后被来至继承文件里的配置重写。 如果发现循环引用，则会报错。

来至所继承配置文件的`files`，`include`和`exclude`*覆盖*源配置文件的属性。

配置文件里的相对路径在解析时相对于它所在的文件。

比如：

`configs/base.json`：

```js
{
  "compilerOptions": {
    "noImplicitAny": true,
    "strictNullChecks": true
  }
}
```

`tsconfig.json`：

```js
{
  "extends": "./configs/base",
  "files": [
    "main.ts",
    "supplemental.ts"
  ]
}
```

`tsconfig.nostrictnull.json`：

```js
{
  "extends": "./tsconfig",
  "compilerOptions": {
    "strictNullChecks": false
  }
}
```

`compileOnSave`

在最顶层设置`compileOnSave`标记，可以让IDE在保存文件的时候根据`tsconfig.json`重新生成文件。

```js
{
    "compileOnSave": true,
    "compilerOptions": {
        "noImplicitAny" : true
    }
}
```

要想支持这个特性需要Visual Studio 2015， TypeScript1.8.4以上并且安装[atom-typescript](https://github.com/TypeStrong/atom-typescript#compile-on-save)插件。