---
translated_at: '2024-03-26T11:54:27.901Z'
---

# 加入

加入操作会等待一组 future 全部准备就绪，并返回它们结果的集合。这类似于 JavaScript 中的 `Promise.all` 或 Python 中的 `asyncio.gather`。

```rust,editable,compile_fail
use anyhow::Result;
use futures::future;
use reqwest;
use std::collections::HashMap;

async fn size_of_page(url: &str) -> Result<usize> {
    let resp = reqwest::get(url).await?;
    Ok(resp.text().await?.len())
}

#[tokio::main]
async fn main() {
    let urls: [&str; 4] = [
        "https://google.com",
        "https://httpbin.org/ip",
        "https://play.rust-lang.org/",
        "BAD_URL",
    ];
    let futures_iter = urls.into_iter().map(size_of_page);
    let results = future::join_all(futures_iter).await;
    let page_sizes_dict: HashMap<&str, Result<usize>> =
        urls.into_iter().zip(results.into_iter()).collect();
    println!("{:?}", page_sizes_dict);
}
```

<details>

将此示例复制到你准备好的 `src/main.rs` 中并从那里运行它。

- 对于多个不同类型的 futures，你可以使用 `std::future::join!`，但你必须在编译时知道你将拥有多少个 futures。这目前位于 `futures` 库中，不久将稳定在 `std::future` 中。

- `join` 的风险是其中一个 future 可能永远不会解析，这会导致你的程序停滞。

- 你也可以将 `join_all` 与 `join!` 结合使用，例如将所有请求加入到 http 服务和数据库查询中。尝试向 future 添加一个 `tokio::time::sleep`，使用 `futures::join!`。这不是超时（那需要 `select!`，将在下一章解释），但演示了 `join!`。

</details>
