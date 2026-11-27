# Agent 入口（我们的 fork）

上游：`BE-Community-Dev/bedrock-world`。本仓库：`XiaoYangx666/bedrock-world`，本地 `/server/mcdev/bedrock-world`。

- 只在本 fork 改，不向上游 push、开 PR、开 issue 或评论
- 依赖 `XiaoYangx666/bedrock-leveldb`（我们的 fork），见 `Cargo.toml`
- 使用方：`/server/mcdev/BEWright/tools/blockwright-world`，固定的 rev 在它的 `Cargo.lock`

## 验证

```sh
cargo test --all-features
```

改动被下游使用时，再到 `/server/mcdev/BEWright/tools/blockwright-world` 跑 `cargo check --locked`。
