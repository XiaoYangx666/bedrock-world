# Agent 入口（我们的 fork）

上游：`BE-Community-Dev/bedrock-world`。本仓库：`XiaoYangx666/bedrock-world`，本地 `/server/mcdev/bedrock-world`。

- 只在本 fork 改，不向上游 push、开 PR、开 issue 或评论
- 依赖 `XiaoYangx666/bedrock-leveldb`（我们的 fork），见 `Cargo.toml`
- 使用方：`/server/mcdev/BEWright/tools/blockwright-world`，固定的 rev 在它的 `Cargo.lock`

## 相对上游的改动

| 改动 | 说明 |
|---|---|
| `from_world_region_blocking` | 每个 subchunk 只解析一次（回读 70 万格 16.1 s → 0.15 s） |
| `compact_storage_blocking_with` | 压实可指定表块大小与 zlib 级别，转发到后端的 `compact_with` |
| `utf8_suffix` | `structuretemplate` / `tickingarea` 的键名改用 UTF-8 后缀（拒绝空串与控制字符）；中文模板名不再被归为 `Unknown`。`map_` 仍走 ASCII 校验 |
| `NbtTag::StringRaw` | `TAG_STRING` 里放二进制（如 `internalComponents…StorageKey`）时保留原始字节，不再判定整条记录解析失败；读写、校验、比较、`NbtRef` / `NbtEvent` 同步支持 |

## 验证

```sh
cargo test --all-features
```

改动被下游使用时，再到 `/server/mcdev/BEWright/tools/blockwright-world` 跑 `cargo check --locked`。
