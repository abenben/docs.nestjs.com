### はじめに


Nest (NestJS) は、効率的でスケーラブルな [Node.js](https://nodejs.org/) サーバサイドアプリケーションを構築するためのフレームワークです。プログレッシブJavaScriptを使用し、[TypeScript](http://www.typescriptlang.org/)を完全にサポートし、OOP（オブジェクト指向プログラミング）、FP（機能的プログラミング）、FRP（機能的反応プログラミング）の要素を組み合わせて構築されています。

<i><font color="silver">Nest (NestJS) is a framework for building efficient, scalable [Node.js](https://nodejs.org/) server-side applications. It uses progressive JavaScript, is built with and fully supports [TypeScript](http://www.typescriptlang.org/) (yet still enables developers to code in pure JavaScript) and combines elements of OOP (Object Oriented Programming), FP (Functional Programming), and FRP (Functional Reactive Programming).</font></i>

Nestは、[Express](https://expressjs.com/)(デフォルト)のような堅牢なHTTPサーバーフレームワークを使用し、オプションで[Fastify](https://github.com/fastify/fastify)も使用できるように設定することが可能です！

<i><font color="silver">Under the hood, Nest makes use of robust HTTP Server frameworks like [Express](https://expressjs.com/) (the default) and optionally can be configured to use [Fastify](https://github.com/fastify/fastify) as well!</font></i>

Nestは、[Express](https://expressjs.com/)(デフォルト)のような堅牢なHTTPサーバーフレームワークを使用し、オプションで[Fastify](https://github.com/fastify/fastify)も使用できるように設定することが可能です！

<i><font color="silver">Nest provides a level of abstraction above these common Node.js frameworks (Express/Fastify), but also exposes their APIs directly to the developer. This gives developers the freedom to use the myriad of third-party modules which are available for the underlying platform.</font></i>

#### 哲学

近年、Node.jsのおかげで、JavaScriptはフロントエンドとバックエンドの両方のアプリケーションでWebの「共通言語」となっています。このため、Angular、React、Vueといった素晴らしいプロジェクトが生まれ、開発者の生産性を向上させ、高速でテスト可能、かつ拡張性の高いフロントエンドアプリケーションの作成を可能にしました。しかし、Node（およびサーバーサイドJavaScript）には優れたライブラリ、ヘルパー、ツールが数多く存在しますが、アーキテクチャという主な問題を効果的に解決するものはありません。

<i><font color="silver">In recent years, thanks to Node.js, JavaScript has become the “lingua franca” of the web for both front and backend applications. This has given rise to awesome projects like [Angular](https://angular.io/), [React](https://github.com/facebook/react) and [Vue](https://github.com/vuejs/vue), which improve developer productivity and enable the creation of fast, testable, and extensible frontend applications. However, while plenty of superb libraries, helpers, and tools exist for Node (and server-side JavaScript), none of them effectively solve the main problem of - **Architecture**.</font></i>

Nestは、開発者やチームがテスト可能でスケーラブル、疎結合で保守しやすいアプリケーションを作成できるようにする、すぐに使えるアプリケーションアーキテクチャを提供します。このアーキテクチャは、Angularに大きくインスパイアされています。

<i><font color="silver">Nest provides an out-of-the-box application architecture which allows developers and teams to create highly testable, scalable, loosely coupled, and easily maintainable applications. The architecture is heavily inspired by Angular.</font></i>

#### インストール

まずは、[Nest CLI](/cli/overview) を使ってプロジェクトを雛形にするか、スタータープロジェクトのクローンを作成します（どちらも同じ結果になります）。

<i><font color="silver">To get started, you can either scaffold the project with the [Nest CLI](/cli/overview), or clone a starter project (both will produce the same outcome).</font></i>

Nest CLIでプロジェクトをscaffoldするには、以下のコマンドを実行します。これにより、新しいプロジェクトディレクトリが作成され、そのディレクトリに初期のコアNestファイルとサポートモジュールが投入され、プロジェクトの従来のベース構造が作成されます。**Nest CLI**を使用して新しいプロジェクトを作成することは、初めて使用する方にお勧めします。この方法は、[ファーストステップ](first-steps)で継続的に説明します。

<i><font color="silver">To scaffold the project with the Nest CLI, run the following commands. This will create a new project directory, and populate the directory with the initial core Nest files and supporting modules, creating a conventional base structure for your project. Creating a new project with the **Nest CLI** is recommended for first-time users. We'll continue with this approach in [First Steps](first-steps).</font></i>

```bash
$ npm i -g @nestjs/cli
$ nest new project-name
```

> info **ヒント:** TypeScript の [strict](https://www.typescriptlang.org/tsconfig#strict) モードを有効にして新しいプロジェクトを作成するには、`nest new` コマンドに `--strict` フラグを渡します。<br><i><font color="gray">To create a new project with TypeScript's [strict](https://www.typescriptlang.org/tsconfig#strict) mode enabled, pass the `--strict` flag to the `nest new` command. </font></i>

#### 代替案

または、TypeScriptスタータープロジェクトを**Git**でインストールすることもできます：

<i><font color="silver">Alternatively, to install the TypeScript starter project with **Git**:</font></i>

```bash
$ git clone https://github.com/nestjs/typescript-starter.git project
$ cd project
$ npm install
$ npm run start
```

> info **ヒント:** gitの履歴を残したままリポジトリをクローンしたい場合は、degitを使用します。<br><i><font color="gray">If you'd like to clone the repository without the git history, you can use [degit](https://github.com/Rich-Harris/degit). </font></i>

ブラウザを開き、[`http://localhost:3000/`](http://localhost:3000/)に移動する。

<i><font color="silver">Open your browser and navigate to [`http://localhost:3000/`](http://localhost:3000/).</font></i>

スタータープロジェクトのJavaScriptフレーバーをインストールするには、上記のコマンドシーケンスで `javascript-starter.git` を使用します。

<i><font color="silver">To install the JavaScript flavor of the starter project, use `javascript-starter.git` in the command sequence above.</font></i>

また、**npm**（または**yarn**）でコアとサポートファイルをインストールすることで、新しいプロジェクトを一から手動で作成することができます。この場合、もちろん、プロジェクトのボイラープレート・ファイルを自分で作成する責任があります。

<i><font color="silver">You can also manually create a new project from scratch by installing the core and supporting files with **npm** (or **yarn**). In this case, of course, you'll be responsible for creating the project boilerplate files yourself.</font></i>

```bash
$ npm i --save @nestjs/core @nestjs/common rxjs reflect-metadata
```
