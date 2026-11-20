# EnvMatrix · 开发环境版本对照

一个单文件的静态网页，把 **Ubuntu LTS / Python / GCC / Clang / ROS 2** 的版本对应关系和支持周期放在一页里。

选版本之前不用翻五个官网——查一眼就知道：这个 Ubuntu 自带哪个 Python、GCC 是哪一版、能不能装某个 ROS 2、离停止维护还有几个月。

**在线预览**：`https://azheng-lab.github.io/devmatrix/`

---

## 为什么做这个

装环境时最常踩的坑，不是命令写错，是**版本对不上**：

- 在 Ubuntu 24.04 上照着一篇 22.04 的教程装 ROS 2 Humble，`apt` 必然 404；
- 用 Ubuntu 20.04 的 GCC 9 学 C++20，一半的新特性编译不过；
- 系统还在支持期，但自带的 Python 早就 EOL 了，长期项目埋雷。

这些信息散在 Ubuntu release notes、python.org、REP-2000、GCC 文档里，每次都要重新查。这个页面把它们并到一起，并且**只做一件事：把「谁支持到什么时候」说清楚**。

## 功能

| 视图 | 作用 |
|---|---|
| 按系统查 | 选一个 Ubuntu LTS，看它自带的 Python / GCC / 默认 ROS 2，以及剩余支持时间 |
| 按语言查 | Python 各版本的 EOL 时间；C 和 C++ 标准分别需要哪个 GCC / Clang |
| 兼容矩阵 | ROS 2 × Ubuntu 的官方对应关系，含已 EOL 的版本 |
| 场景推荐 | 「学 Python / 刷题 / 学 ROS 2 / 跑深度学习 / 长期项目」分别该用哪个版本 |
| 全局搜索 | 输入 `22.04`、`3.12`、`jazzy`、`gcc 11`、`c++20` 直接跳转 |

## 运行

没有任何依赖，也没有构建步骤。

```bash
git clone <repo>
cd devmatrix
# 直接双击 index.html，或者：
python -m http.server 8000
```

## 部署到 GitHub Pages

1. 新建仓库 `devmatrix`，把 `index.html` 推到 `main` 分支
2. Settings → Pages → Source 选 `Deploy from a branch`，分支 `main`，目录 `/ (root)`
3. 等一分钟，访问 `https://<用户名>.github.io/devmatrix/`

## 数据来源

- Ubuntu 版本与支持周期：[Ubuntu release notes](https://wiki.ubuntu.com/Releases)，标准支持 5 年 + Ubuntu Pro 扩展 5 年
- Python 版本与 EOL：[devguide](https://devguide.python.org/versions/)
- ROS 2 发行版：[REP-2000](https://www.ros.org/reps/rep-2000.html)
- C / C++ 标准支持：[GCC standards support](https://gcc.gnu.org/projects/cxx-status.html)、[Clang C status](https://clang.llvm.org/c_status.html)

「自带版本」指该 Ubuntu 版本仓库中的默认 `python3` / `gcc`，实际可能因 update 有小幅差异。

**校对日期：2026-11-19**。发现错误欢迎提 issue。

## 设计取舍

- **只到月，不到日**：版本 EOL 精确到天没有意义，反而制造假精确，所以统一用 `YYYY-MM`。
- **不猜**：数据写死在 `index.html` 顶部的 `OS` / `PY` / `ROS` / `CSTD` / `CXXSTD` 数组里，要改就改数组，不引入构建工具。
- **单文件**：一个 HTML 能当作品集、能挂 Pages、能发给别人双击打开。

## License

MIT
