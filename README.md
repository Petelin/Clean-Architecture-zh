# Clean-Architecture-zh

《架构整洁之道》中文翻译

在线阅读：[http://gdut_yy.gitee.io/doc-cleanarch/](http://gdut_yy.gitee.io/doc-cleanarch/)

<img src="./docs/cover.jpg" width=24% />

## 目录

- [第一部分 概述](docs/part1.md)
- [第 1 章 设计与架构究竟是什么](docs/ch1.md)
- [第 2 章 两个价值维度](docs/ch2.md)

---

- [第二部分 从基础构件开始：编程范式](docs/part2.md)
- [第 3 章 编程范式总览](docs/ch3.md)
- [第 4 章 结构化编程](docs/ch4.md)
- [第 5 章 面向对象编程](docs/ch5.md)
- [第 6 章 函数式编程](docs/ch6.md)

---

- [第三部分 设计原则](docs/part3.md)
- [第 7 章 SRP：单一职责原则](docs/ch7.md)
- [第 8 章 OCP：开闭原则](docs/ch8.md)
- [第 9 章 LSP：里氏替换原则](docs/ch9.md)
- [第 10 章 ISP：接口隔离原则](docs/ch10.md)
- [第 11 章 DIP：依赖反转原则](docs/ch11.md)

---

- [第四部分 组件构建原则](docs/part4.md)
- [第 12 章 组件](docs/ch12.md)
- [第 13 章 组件聚合](docs/ch13.md)
- [第 14 章 组件耦合](docs/ch14.md)

---

- [第五部分 软件架构](docs/part5.md)
- [第 15 章 什么是软件架构](docs/ch15.md)
- [第 16 章 独立性](docs/ch16.md)
- [第 17 章 划分边界](docs/ch17.md)
- [第 18 章 边界剖析](docs/ch18.md)
- [第 19 章 策略与层次](docs/ch19.md)
- [第 20 章 业务逻辑](docs/ch20.md)
- [第 21 章 尖叫的软件架构](docs/ch21.md)
- [第 22 章 整洁架构](docs/ch22.md)
- [第 23 章 展示器和谦卑对象](docs/ch23.md)
- [第 24 章 不完全边界](docs/ch24.md)
- [第 25 章 层次与边界](docs/ch25.md)
- [第 26 章 Main 组件](docs/ch26.md)
- [第 27 章 服务：宏观和微观](docs/ch27.md)
- [第 28 章 测试边界](docs/ch28.md)
- [第 29 章 整洁的嵌入式架构](docs/ch29.md)

---

- [第六部分 实现细节](docs/part6.md)
- [第 30 章 数据库只是实现细节](docs/ch30.md)
- [第 31 章 Web 是实现细节](docs/ch31.md)
- [第 32 章 应用程序框架是实现细节](docs/ch32.md)
- [第 33 章 案例分析：视频销售网站](docs/ch33.md)
- [第 34 章 拾遗](docs/ch34.md)

## 本地开发 & 阅读

本项目基于 vuepress 进行开发，以提供比 github mardown 更佳的阅读体验

依赖于 `node.js`、`yarn`、`vuepress` 等环境

```sh
# vuepress
yarn global add vuepress

# 本地开发
git clone https://github.com/gdut-yy/Clean-Architecture-zh.git
cd Clean-Architecture-zh/
yarn docs:dev
```

## Contributors

<table>
  <tr>
    <td align="center"><a href="https://gdut-yy.github.io/"><img src="https://avatars2.githubusercontent.com/u/33390928?s=460&v=4" width="100px;" /><br /><sub><b>gdut-yy</b></sub></a><br /></td>
    <td align="center"><a href="https://github.com/qisixian"><img src="https://avatars1.githubusercontent.com/u/24975483?s=460&u=a73b906e48207589087676dfb567207ae93b66ac&v=4" width="100px;" /><br /><sub><b>qisixian</b></sub></a><br /></td>
    <td align="center"><a href="https://github.com/latavin243"><img src="https://avatars0.githubusercontent.com/u/16208315?s=460&u=c4a46e233583bc687fa59c863dd0f144e9f5664b&v=4" width="100px;" /><br /><sub><b>qguo</b></sub></a><br /></td>
    <td align="center"><a href="https://github.com/oldfatcrab"><img src="https://avatars2.githubusercontent.com/u/1563274?s=460&v=4" width="100px;" /><br /><sub><b>oldfatcrab</b></sub></a><br /></td>
    <td align="center"><a href="https://github.com/venthent"><img src="https://avatars2.githubusercontent.com/u/35421630?s=460&u=753b74ddd9c7df2bfa9c0833dccd821e15baac42&v=4" width="100px;" /><br /><sub><b>venthent</b></sub></a><br /></td>
    <td align="center"><a href="https://github.com/ZhuPeng"><img src="https://avatars1.githubusercontent.com/u/4994339?s=460&u=5d9b3258f58b4e8df6e8906cee02a7529df3fa50&v=4" width="100px;" /><br /><sub><b>ZhuPeng</b></sub></a><br /></td>
    <td align="center"><a href="https://github.com/falconwoo"><img src="https://avatars2.githubusercontent.com/u/11451271?s=400&v=4" width="100px;" /><br /><sub><b>falconwoo</b></sub></a><br /></td>
  </tr>
    <tr>
    <td align="center"><a href="https://github.com/zerosoul"><img src="https://avatars0.githubusercontent.com/u/2985895?s=400&u=8f9efe4bde312c7935697c0b4024489c9913c26b&v=4" width="100px;" /><br /><sub><b>zerosoul</b></sub></a><br /></td>
    <td align="center"><a href="https://github.com/wuwen1030"><img src="https://avatars1.githubusercontent.com/u/3377567?s=460&u=495e60f96d9ac1ea3dedcd0651d2862cae2e3125&v=4" width="100px;" /><br /><sub><b>wuwen1030</b></sub></a><br /></td>
  </tr>
</table>

## 更多书籍

[https://github.com/xx-zh/xx-zh-roadmap](https://github.com/xx-zh/xx-zh-roadmap)

## License

[MIT](./LICENSE)
