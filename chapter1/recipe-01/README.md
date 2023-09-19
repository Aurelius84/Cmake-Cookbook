# 入门

CMake 不强制指定构建目录执行名称或位置，我们完全可以把它放在项目路径之外。这样做同样有效：
```bash
$ mkdir -p /tmp/someplace
$ cd /tmp/someplace
$ cmake /path/to/source
$ cmake --build .
```

## 1.2 切换生成器

必须显式地使用命令行方式，用 `-G` 切换生成器。
```bash
$ cmake -GNinja ..
```

注：
    + 按照原文使用 `cmake -G Ninja ..`命令，在MacOs下会报`CMake Error: Could not create named generator Ninjia`。
    + 如果遇到 cmake 找不到 Ninja，也可尝试把 CMakeCache.txt 给删除下，包括依赖的third_party 目录下的

