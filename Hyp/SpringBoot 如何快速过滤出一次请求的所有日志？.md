---
doc_type: hypothesis-highlights
url: 'https://mp.weixin.qq.com/s/mHAlsC3h2xg_93KdFj3mOA'
---

# SpringBoot 如何快速过滤出一次请求的所有日志？

## Metadata
- Author: [mp.weixin.qq.com]()
- Title: SpringBoot 如何快速过滤出一次请求的所有日志？
- Reference: https://mp.weixin.qq.com/s/mHAlsC3h2xg_93KdFj3mOA
- Category: #article

## Page Notes
## Highlights
- 由于这个逻辑之间没有强耦合的关系，所以通常是异步处理。如何将一次数据上报请求中包含的所有业务日志快速过滤出来，就是本文要介绍的 — [Updated on 2022-12-26 14:51:18](https://hyp.is/s0RCVITpEe2hHJegk1asYQ/mp.weixin.qq.com/s/mHAlsC3h2xg_93KdFj3mOA) — Group: #Public
    - Annotation: 
- [ ] SLF4J 日志框架提供了 MDC 工具类，用来快速过滤一次请求的所有日志，并通过装饰器模式使得MDC工具在异步线程里也能生效。


