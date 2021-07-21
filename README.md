This is a [Next.js](https://nextjs.org/) project bootstrapped with [`create-next-app`](https://github.com/vercel/next.js/tree/canary/packages/create-next-app).

This project is aimed to demonstrate how to implement a Serverless Functions working with Webassembly in Vercel. The [main branch](https://github.com/second-state/vercel-wasm-runtime/tree/main) showcases an image processing function, and the [tensorflow branch](https://github.com/second-state/vercel-wasm-runtime/tree/tensorflow) showcases an AI inference function. Both written in simple Rust and runs in the [WasmEdge runtime](https://github.com/WasmEdge/WasmEdge) for WebAssembly.

## Overview

The Serverless Functions endpoint is located at `api/hello.js` to meet the requirement of Vercel, but not to the Next.js. So if you want to develop on you local machine, you should put it into `pages/api/` and make some change.

The only function in `api/hello.js` is classifying the object in a photo. It receives a jpg file and pass it as stdin stream to a spawned child process. The child process runs using the [wasmedge-tensorflow-lite](https://github.com/second-state/WasmEdge-tensorflow-tools) command.

File `api/functions/image-classification/src/main.rs` implements the tensorflow-based image recognition logic. You can build it with the Rust `cargo` command with the `-target wasm32-wasi` option to get the `classify.wasm` file.

We define [Custom Build](https://vercel.com/docs/runtimes?query=vercel-build#advanced-usage/advanced-node-js-usage/custom-build-step-for-node-js) in `api/pre.sh` to download the [wasmedge-tensorflow-lite command and dependent lib](https://github.com/second-state/WasmEdge-tensorflow-tools#run-wasmedge-tensorflow-tools).

![](/vercel-wasmedge-runtime.gif)


## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.

You can check out [the Next.js GitHub repository](https://github.com/vercel/next.js/) - your feedback and contributions are welcome!

To learn more about Serverless Functions in Vercel, take a look at the following resources:

- [Serverless Functions](https://vercel.com/docs/serverless-functions/introduction) - how to write your Serverless Functions.
- [Runtime](https://vercel.com/docs/runtimes) - the modules that lift Serverless Functions.

## Deploy on Vercel

The easiest way to deploy your Next.js app is to use the [Vercel Platform](https://vercel.com/import?utm_medium=default-template&filter=next.js&utm_source=create-next-app&utm_campaign=create-next-app-readme) from the creators of Next.js.

Check out our [Next.js deployment documentation](https://nextjs.org/docs/deployment) for more details.
