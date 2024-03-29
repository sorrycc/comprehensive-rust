---
translated_at: '2024-03-26T11:53:32.616Z'
---

# 选择

`select` 操作等待一组未来（futures）中的任何一个准备就绪，并对该未来的结果做出响应。在 JavaScript 中，这类似于 `Promise.race`。在 Python 中，它与 `asyncio.wait(task_set, return_when=asyncio.FIRST_COMPLETED)` 相似。

类似于 `match` 语句，`select!` 的主体有多个分支，每个分支的形式为 `pattern = future => statement`。当一个 `future` 准备就绪时，其返回值被 `pattern` 解构。然后执行含有结果变量的 `statement`。`statement` 的结果成为 `select!` 宏的结果。

```rust,editable,compile_fail
use tokio::sync::mpsc::{self, Receiver};
use tokio::time::{sleep, Duration};

#[derive(Debug, PartialEq)]
enum Animal {
    Cat { name: String },
    Dog { name: String },
}

async fn first_animal_to_finish_race(
    mut cat_rcv: Receiver<String>,
    mut dog_rcv: Receiver<String>,
) -> Option<Animal> {
    tokio::select! {
        cat_name = cat_rcv.recv() => Some(Animal::Cat { name: cat_name? }),
        dog_name = dog_rcv.recv() => Some(Animal::Dog { name: dog_name? })
    }
}

#[tokio::main]
async fn main() {
    let (cat_sender, cat_receiver) = mpsc::channel(32);
    let (dog_sender, dog_receiver) = mpsc::channel(32);
    tokio::spawn(async move {
        sleep(Duration::from_millis(500)).await;
        cat_sender.send(String::from("Felix")).await.expect("未能发送猫消息。");
    });
    tokio::spawn(async move {
        sleep(Duration::from_millis(50)).await;
        dog_sender.send(String::from("Rex")).await.expect("未能发送狗消息。");
    });

    let winner = first_animal_to_finish_race(cat_receiver, dog_receiver)
        .await
        .expect("未能接收到胜者");

    println!("胜者是 {winner:?}");
}
```

<details>

- 在这个例子中，我们设有一场猫和狗之间的比赛。`first_animal_to_finish_race` 监听两个频道，并将选择先到达的那个。由于狗只需要 50ms，因此它赢了需要 500ms 的猫。

- 在此例中你可以使用 `oneshot` 通道，因为这些通道预期将

```markdown
  只能接收一次 `send`。

- 尝试为比赛添加一个截止日期，演示选择不同种类的
  期货。

- 注意 `select!` 会丢弃不匹配的分支，这会取消它们的期货。当每次执行 `select!` 都创建新的期货时，使用它最为简单。

  - 另一种方法是传递 `&mut future` 而不是期货本身，但是
    这可能会导致问题，在固定幻灯片中有进一步的讨论。

</details>
```
