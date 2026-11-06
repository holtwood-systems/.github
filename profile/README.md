# Holtwood Systems

个人维护者：[holtwood](https://github.com/holtwood) · AI Infra / HPC systems

从可验证的 CUDA/Triton kernel，到真实权重推理运行时与 Rust serving 控制面。

**入口**：[portfolio](https://github.com/holtwood-systems/portfolio) · [项目总览](https://imshane.site/projects)

## 旗舰系统

**[paged-serving](https://github.com/holtwood-systems/paged-serving) 控制面**通过受测试的同进程 C ABI 调用 **[tiny-llm](https://github.com/holtwood-systems/tiny-llm) 数据面**：

```text
HTTP/SSE → continuous batching → Paged KV/block tables
                                      ⇅ C ABI
                              GGUF/W8A16 → CUDA decode
```

这是一个端到端项目，用两个仓库表达控制面/数据面边界，不是两个孤立 demo。

## 项目地图

| 角色 | 仓库 | 重点 | 状态 |
|------|------|------|------|
| 总入口 | [portfolio](https://github.com/holtwood-systems/portfolio) | 作品集、学习路径、证据索引与跨仓契约 | active |
| 旗舰控制面 | [paged-serving](https://github.com/holtwood-systems/paged-serving) | 调度、Paged KV、HTTP/SSE、serving 评测 | active |
| 旗舰数据面 | [tiny-llm](https://github.com/holtwood-systems/tiny-llm) | 真实权重、量化、decode、KV、C ABI | active |
| CUDA 深挖 | [cuflash](https://github.com/holtwood-systems/cuflash) | FlashAttention 前后向、Tensor Core、FlashDecoding | stable |
| Triton 对照 | [trifuse](https://github.com/holtwood-systems/trifuse) | 融合算子、参考实现、`torch.library` | stable |
| CUDA 基础 | [cuda-foundations](https://github.com/holtwood-systems/cuda-foundations) | SGEMM 优化阶梯与可复用推理组件 | stable |
| C++ 教学 | [cpp-high-performance-guide](https://github.com/holtwood-systems/cpp-high-performance-guide) | C++20 性能工程：内存、SIMD、并发、NUMA、GEMM 案例 | stable |
| 上游研究 | [kvtier](https://github.com/holtwood-systems/kvtier) | SGLang HiCache/KV tiering 复现实验与上游贡献 | active |

## 从哪里开始

- [portfolio：作品集与导航](https://github.com/holtwood-systems/portfolio)
- [可追溯证据与当前缺口](https://github.com/holtwood-systems/portfolio/blob/master/docs/evidence-index.md)
- [完整学习路径](https://github.com/holtwood-systems/portfolio/blob/master/LEARNING_PATH.md)
- [跨仓语义与 ABI 契约](https://github.com/holtwood-systems/portfolio/blob/master/docs/cross-repo-contracts.md)

## 工程原则

- **可追溯性能证据**：数字绑定硬件、commit、复现命令、原始结果与限制
- **差分测试**：优化实现与独立参考实现做数值对比
- **不变量验证**：检查 KV Cache 资源守恒、调度状态机与跨语言布局
- **边界先于宣传**：CPU 参考、本地 smoke 和真实 GPU Serving 结果分开表述

---

维护者：[holtwood](https://github.com/holtwood) · 项目总览：[imshane.site/projects](https://imshane.site/projects)
相关组织：[holtwood-arena](https://github.com/holtwood-arena)（比赛与 benchmark） · [holtwood-forks](https://github.com/holtwood-forks)（上游研读）
