---
translated_at: '2024-03-26T10:49:11.208Z'
---

# 多线程链接检查器

让我们利用新学到的知识创建一个多线程链接检查器。它应该从一个网页开始，检查页面上的链接是否有效。它应该递归检查同一域名上的其他页面，并继续这样做直到所有页面都被验证。

为此，你将需要一个 HTTP 客户端，比如 [`reqwest`][1]。你还需要一种找到链接的方法，我们可以使用 [`scraper`][2]。最后，我们需要一些错误处理的方式，我们将使用 [`thiserror`][3]。

创建一个新的 Cargo 项目并将 `reqwest` 添加为依赖：

```shell
cargo new link-checker
cd link-checker
cargo add --features blocking,rustls-tls reqwest
cargo add scraper
cargo add thiserror
```

> 如果 `cargo add` 命令失败并出现 `error: no such subcommand` 的错误，那么请手动编辑 `Cargo.toml` 文件。添加下面列出的依赖。

`cargo add` 调用会更新 `Cargo.toml` 文件，使其看起来像这样：

<!-- File Cargo.toml -->

```toml
[package]
name = "link-checker"
version = "0.1.0"
edition = "2021"
publish = false

[dependencies]
reqwest = { version = "0.11.12", features = ["blocking", "rustls-tls"] }
scraper = "0.13.0"
thiserror = "1.0.37"
```

现在你可以下载开始页面了。试试一个小网站，比如 `https://www.google.org/`。

你的 `src/main.rs` 文件应该看起来像这样：

<!-- File src/main.rs -->

```rust,compile_fail
{{#include link-checker.rs:setup}}

{{#include link-checker.rs:visit_page}}

fn main() {
    let client = Client::new();
    let start_url = Url::parse("https://www.google.org").unwrap();
    let crawl_command = CrawlCommand{ url: start_url, extract_links: true };
    match visit_page(&client, &crawl_command) {
        Ok(links) => println!("链接：{links:#?}"),
        Err(err) => println!("无法提取链接：{err:#}"),
    }
}
```

使用以下命令运行 `src/main.rs` 中的代码：

```shell
cargo run
```

## 任务

- 使用线程并行检查链接：将待检查的 URL 发送到一个通道，并让几个线程并行检查 URL。
- 扩展这个功能以递归提取同一域名上所有页面的链接。

  `www.google.org` 域名。设置大约 100 页的上限，以免最终被网站封禁。

[1]: https://docs.rs/reqwest/
[2]: https://docs.rs/scraper/
[3]: https://docs.rs/thiserror/
