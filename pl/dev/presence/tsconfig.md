---
title: TypeScript Configuration
description: A little helper for TypeScript
published: true
date: 2021-12-20T14:27:18.034Z
tags:
editor: markdown
dateCreated: 2021-09-07T01:45:10.473Z
---

# TypeScript Configuration

## Wprowadzenie

When you downloaded and unpacked the workspace, you will see a file called `tsconfig.json` in root and presence folders, this file is used for configuring the **TypeScript** compiler. It is already configured for you, so don't worry about that.

We just want to describe some settings that you should know.

## Root Configuration

In the root configuration file you will see something like this.

```json
{
  "compilerOptions": {
    "module": "CommonJS",
    "target": "ES2020",
    "removeComments": true,
    "noEmitOnError": true,
    "noFallthroughCasesInSwitch": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "inlineSourceMap": true,
    "typeRoots": ["@types"],
    "esModuleInterop": true
  }
}
```

| Property                   | Opis                                                                                                                                                                |
|:-------------------------- |:------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **compilerOptions**        | Used for configuring the compiler, most of the properties are located here.                                                                                         |
| module                     | You can read more about that [here](https://www.typescriptlang.org/docs/handbook/modules.html).                                                                     |
| target                     | Defines the JavaScript version you are compiling.                                                                                                                   |
| removeComments             | Removing comments from compiled files.                                                                                                                              |
| noEmitOnError              | Do not emit outputs if any errors were reported.                                                                                                                    |
| noFallthroughCasesInSwitch | Zgłasza błędy dla przypadków awaryjnych w instrukcji switch.                                                                                                        |
| noUnusedLocals             | Zgłasza błędy na nieużywanych lokalnych.                                                                                                                            |
| noUnusedParameters         | Zgłasza błędy dotyczące nieużywanych parametrów.                                                                                                                    |
| inlineSourceMap            | Dodaje sourcemapping                                                                                                                                                |
| typeRoots                  | Więcej na ten temat znajdziesz [tu](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html#types-typeroots-and-types).                                     |
| esModuleInterop            | Emit __importStar and __importDefault helpers for runtime babel ecosystem compatibility and enable --allowSyntheticDefaultImports for typesystem compatibility. |

## Presence Configuration

```json
{
  "extends": "../../../tsconfig.json",
  "compilerOptions": {
    "outDir": "./dist/"
  }
}
```

| Property            | Opis                                                                                   |
|:------------------- |:-------------------------------------------------------------------------------------- |
| **extends**         | Used for extending the base `tsconfig` file for various tasks.                         |
| **compilerOptions** | See [**Root Configuration**](/dev/presence/tsconfig#root-configuration) for more info. |
| outDir              | Defines the output directory for compiled files.                                       |
