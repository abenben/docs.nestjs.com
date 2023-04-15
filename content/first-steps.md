### ファーストステップ（First steps）

この一連の記事では、Nestの中核となる基礎知識を学びます。Nestアプリケーションの本質的な構成要素に慣れるために、入門レベルで多くの領域をカバーする機能を備えた基本的なCRUDアプリケーションを構築します。

In this set of articles, you'll learn the **core fundamentals** of Nest. To get familiar with the essential building blocks of Nest applications, we'll build a basic CRUD application with features that cover a lot of ground at an introductory level.

#### 言語（Language）

私たちはTypeScriptを愛していますが、何よりもNode.jsを愛しています。そのため、NestはTypeScriptと純粋なJavaScriptの両方と互換性があります。Nestは最新の言語機能を利用しているので、バニラJavaScriptで使用するにはBabelコンパイラが必要です。

We're in love with [TypeScript](https://www.typescriptlang.org/), but above all - we love [Node.js](https://nodejs.org/en/). That's why Nest is compatible with both TypeScript and **pure JavaScript**. Nest takes advantage of the latest language features, so to use it with vanilla JavaScript we need a [Babel](https://babeljs.io/) compiler.

提供するサンプルでは主にTypeScriptを使用しますが、コードスニペットをバニラJavaScriptの構文に切り替えることができます（各スニペットの右上にある言語ボタンをクリックして切り替えるだけです）。

We'll mostly use TypeScript in the examples we provide, but you can always **switch the code snippets** to vanilla JavaScript syntax (simply click to toggle the language button in the upper right hand corner of each snippet).

#### 前提条件（Prerequisites）

Node.js（バージョン >= 12、v13を除く）がOSにインストールされていることを確認してください。

Please make sure that [Node.js](https://nodejs.org) (version >= 12, except for v13) is installed on your operating system.

#### セットアップ（Setup）

Nest CLIを使えば、新しいプロジェクトのセットアップは非常に簡単です。npmをインストールした状態で、OSのターミナルで以下のコマンドを実行すると、新しいNestプロジェクトを作成することができます：

Setting up a new project is quite simple with the [Nest CLI](/cli/overview). With [npm](https://www.npmjs.com/) installed, you can create a new Nest project with the following commands in your OS terminal:

```bash
$ npm i -g @nestjs/cli
$ nest new project-name
```

> info **ヒント** TypeScriptの[strict](https://www.typescriptlang.org/tsconfig#strict)モードを有効にして新しいプロジェクトを作成するには、`nest new`コマンドに`--strict`フラグを渡します。<br>To create a new project with TypeScript's [strict](https://www.typescriptlang.org/tsconfig#strict) mode enabled, pass the `--strict` flag to the `nest new` command. 

project-name`ディレクトリが作成され、nodeモジュールと他のいくつかのボイラープレートファイルがインストールされ、`src/`ディレクトリが作成され、いくつかのコアファイルが配置されることになります。

The `project-name` directory will be created, node modules and a few other boilerplate files will be installed, and a `src/` directory will be created and populated with several core files.

<div class="file-tree">
  <div class="item">src</div>
  <div class="children">
    <div class="item">app.controller.spec.ts</div>
    <div class="item">app.controller.ts</div>
    <div class="item">app.module.ts</div>
    <div class="item">app.service.ts</div>
    <div class="item">main.ts</div>
  </div>
</div>

ここでは、それらのコアファイルの概要を説明します：

Here's a brief overview of those core files:

|                          |                                                                                                                     |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------- |
| `app.controller.ts`      | A basic controller with a single route.                                                                             |
| `app.controller.spec.ts` | The unit tests for the controller.                                                                                  |
| `app.module.ts`          | The root module of the application.                                                                                 |
| `app.service.ts`         | A basic service with a single method.                                                                               |
| `main.ts`                | The entry file of the application which uses the core function `NestFactory` to create a Nest application instance. |

main.ts`には非同期関数があり、これがアプリケーションの**bootstrap**となります：

The `main.ts` includes an async function, which will **bootstrap** our application:

```typescript
@@filename(main)

import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(3000);
}
bootstrap();
@@switch
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(3000);
}
bootstrap();
```

Nestアプリケーションのインスタンスを作成するには、コアとなる `NestFactory` クラスを使用します。NestFactory` は、アプリケーションインスタンスを作成するためのいくつかの静的メソッドを公開しています。create()`メソッドは、`INestApplication` インターフェースを満たすアプリケーションオブジェクトを返します。このオブジェクトは、これからの章で説明する一連のメソッドを提供します。上の `main.ts` の例では、HTTPリスナーを起動するだけで、アプリケーションが受信したHTTPリクエストを待ち受けることができます。

To create a Nest application instance, we use the core `NestFactory` class. `NestFactory` exposes a few static methods that allow creating an application instance. The `create()` method returns an application object, which fulfills the `INestApplication` interface. This object provides a set of methods which are described in the coming chapters. In the `main.ts` example above, we simply start up our HTTP listener, which lets the application await inbound HTTP requests.

Nest CLIを使用して雛形化されたプロジェクトは、開発者が各モジュールを専用のディレクトリに保持する慣習に従うことを奨励する初期プロジェクト構造を作成することに注意してください。

Note that a project scaffolded with the Nest CLI creates an initial project structure that encourages developers to follow the convention of keeping each module in its own dedicated directory.

> info **ヒント** By default, if any error happens while creating the application your app will exit with the code `1`. If you want to make it throw an error instead disable the option `abortOnError` (e.g., `NestFactory.create(AppModule, {{ '{' }} abortOnError: false {{ '}' }})`).

<app-banner-courses></app-banner-courses>

#### プラットフォーム

Nestは、プラットフォームに依存しないフレームワークであることを目指しています。プラットフォームに依存しないことで、開発者が複数の異なるタイプのアプリケーションで活用できる、再利用可能な論理パーツを作成することが可能になります。技術的には、Nestは、アダプタを作成すれば、どのNode HTTPフレームワークでも動作させることが可能です。すぐに使えるHTTPプラットフォームは2つあります： [express](https://expressjs.com/)と[fastify](https://www.fastify.io)です。あなたのニーズに最も適したものを選択することができます。

Nest aims to be a platform-agnostic framework. Platform independence makes it possible to create reusable logical parts that developers can take advantage of across several different types of applications. Technically, Nest is able to work with any Node HTTP framework once an adapter is created. There are two HTTP platforms supported out-of-the-box: [express](https://expressjs.com/) and [fastify](https://www.fastify.io). You can choose the one that best suits your needs.

|                    |                                                                                                                                                                                                                                                                                                                                    |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `platform-express` | [Express](https://expressjs.com/) is a well-known minimalist web framework for node. It's a battle tested, production-ready library with lots of resources implemented by the community. The `@nestjs/platform-express` package is used by default. Many users are well served with Express, and need take no action to enable it. |
| `platform-fastify` | [Fastify](https://www.fastify.io/) is a high performance and low overhead framework highly focused on providing maximum efficiency and speed. Read how to use it [here](/techniques/performance).                                                                                                                                  |

どちらのプラットフォームを利用する場合でも、独自のアプリケーションインターフェースを公開します。これらはそれぞれ `NestExpressApplication` と `NestFastifyApplication` として参照されます。

Whichever platform is used, it exposes its own application interface. These are seen respectively as `NestExpressApplication` and `NestFastifyApplication`.

以下の例のように `NestFactory.create()` メソッドに型を渡すと、`app` オブジェクトはそのプラットフォーム専用のメソッドを持つことになります。ただし、実際にプラットフォームのAPIにアクセスするのでなければ、型を指定する必要はありません。

When you pass a type to the `NestFactory.create()` method, as in the example below, the `app` object will have methods available exclusively for that specific platform. Note, however, you don't **need** to specify a type **unless** you actually want to access the underlying platform API.

```typescript
const app = await NestFactory.create<NestExpressApplication>(AppModule);
```

#### アプリケーションを実行する（Running the application）

インストールが完了したら、OSのコマンドプロンプトで以下のコマンドを実行することで、アプリケーションがHTTPのインバウンドリッスンを開始することができます：

Once the installation process is complete, you can run the following command at your OS command prompt to start the application listening for inbound HTTP requests:

```bash
$ npm run start
```

このコマンドは、`src/main.ts`ファイルで定義されたポートでHTTPサーバーをリッスンする状態でアプリを起動します。アプリケーションが起動したら、ブラウザを開いて`http://localhost:3000/`に移動してください。すると、`Hello World!`というメッセージが表示されるはずです。

This command starts the app with the HTTP server listening on the port defined in the `src/main.ts` file. Once the application is running, open your browser and navigate to `http://localhost:3000/`. You should see the `Hello World!` message.

ファイルの変更を監視するために、次のコマンドを実行してアプリケーションを起動することができます：

To watch for changes in your files, you can run the following command to start the application:

```bash
$ npm run start:dev
```

このコマンドは、ファイルを監視し、自動的に再コンパイルとサーバーの再読み込みを行います。

This command will watch your files, automatically recompiling and reloading the server.
