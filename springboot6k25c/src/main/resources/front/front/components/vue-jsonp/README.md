**项目简介：**  
本项目基于主流的前后端分离架构，采用 **SpringBoot + Vue 技术栈**，配套 **MySQL 数据库**，适用于毕业设计与课题实训开发。  
本人已整理了超 **4000 多套毕业设计源码+论文+开题报告+PPT...**，涵盖 **Java、SpringBoot、Vue、SSM、uni-app 小程序、PHP、Android** 等方向，支持功能修改定制与论文服务。  
**团队提供以下服务：**  
- 项目代码修改与调试  
- 数据库配置与远程协助  
- 论文定制与修改  
**获取更多的4000多套源码或SQL文件请联系：**  
- QQ：3906443360 微信：BesheHelp


# vue-jsonp

# Vue-jsonp

[![VueJsonp](https://github.com/LancerComet/vue-jsonp/workflows/Test/badge.svg)](https://github.com/LancerComet/vue-jsonp/actions)

A tiny library for handling JSONP request.

## Quick Start

As Vue plugin:

```ts
import { VueJsonp } from 'vue-jsonp'

// Vue Plugin.
Vue.use(VueJsonp)

// Now you can use this.$jsonp in Vue components.
const vm = new Vue()
vm.$jsonp('/some-jsonp-url', {
  myCustomUrlParam: 'veryNice'
})
```

Use function directly:

```ts
import { jsonp } from 'vue-jsonp'

jsonp('/some-jsonp-url', {
  myCustomUrlParam: 'veryNice'
})
```

## Send data and set query & function name

### Send data

```ts
// The request url will be "/some-jsonp-url?name=LancerComet&age=100&callback=jsonp_{RANDOM_STR}".
jsonp('/some-jsonp-url', {
  name: 'LancerComet',
  age: 100
})
```

### Custom query & function name

The url uniform is `/url?{callbackQuery}={callbackName}&...`, the default is `/url?callback=jsonp_{RANDOM_STRING}&...`.

And you can change it like this:

```ts
// The request url will be "/some-jsonp-url?name=LancerComet&age=100&cb=jsonp_func".
jsonp('/some-jsonp-url', {
  callbackQuery: 'cb',
  callbackName: 'jsonp_func',
  name: 'LancerComet',
  age: 100
})
```

## Module exports

 - `VueJsonp: PluginObject<never>`
 
 - `jsonp<T>: (url: string, param?: IJsonpParam, timeout?: number) => Promise<T>`
 
## API

### IJsonpParam

IJsonpParam is the type of param for jsonp function.

```ts
/**
 * JSONP parameter declaration.
 */
interface IJsonpParam {
  /**
   * Callback query name.
   * This param is used to define the query name of the callback function.
   *
   * @example
   * // The request url will be "/some-url?myCallback=jsonp_func&myCustomUrlParam=veryNice"
   * jsonp('/some-url', {
   *   callbackQuery: 'myCallback',
   *   callbackName: 'jsonp_func',
   *   myCustomUrlParam: 'veryNice'
   * })
   *
   * @default callback
   */
  callbackQuery?: string

  /**
   * Callback function name.
   * This param is used to define the jsonp function name.
   *
   * @example
   * // The request url will be "/some-url?myCallback=jsonp_func&myCustomUrlParam=veryNice"
   * jsonp('/some-url', {
   *   callbackQuery: 'myCallback',
   *   callbackName: 'jsonp_func',
   *   myCustomUrlParam: 'veryNice'
   * })
   *
   * @default jsonp_ + randomStr()
   */
  callbackName?: string

  /**
   * Custom data.
   */
  [key: string]: any
}
```

## Example

```ts
import Vue from 'vue'
import { VueJsonp } from 'vue-jsonp'

Vue.use(VueJsonp)

const vm = new Vue()
const { code, data, message } = await vm.$jsonp<{
  code: number,
  message: string,
  data: {
    id: number,
    nickname: string
  }
}>('/my-awesome-url', {
  name: 'MyName', age: 20
})

assert(code === 0)
assert(message === 'ok')
assert(data.id === 1)
assert(data.nickname === 'John Smith')
```

```ts
import { jsonp } from 'vue-jsonp'

const result = await jsonp<string>('/my-awesome-url')
assert(result === 'such a jsonp')
```

## License

MIT
