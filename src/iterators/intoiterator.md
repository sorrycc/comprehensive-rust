---
minutes: 5
translated_at: '2024-03-26T10:42:52.895Z'
---

# `IntoIterator`

`Iterator` trait 告诉你一旦创建了迭代器该如何 _迭代_。相关 trait
[`IntoIterator`](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html)
定义了如何为一个类型创建迭代器。它会被 `for` 循环自动使用。

```rust,editable
struct Grid {
    x_coords: Vec<u32>,
    y_coords: Vec<u32>,
}

impl IntoIterator for Grid {
    type Item = (u32, u32);
    type IntoIter = GridIter;
    fn into_iter(self) -> GridIter {
        GridIter { grid: self, i: 0, j: 0 }
    }
}

struct GridIter {
    grid: Grid,
    i: usize,
    j: usize,
}

impl Iterator for GridIter {
    type Item = (u32, u32);

    fn next(&mut self) -> Option<(u32, u32)> {
        if self.i >= self.grid.x_coords.len() {
            self.i = 0;
            self.j += 1;
            if self.j >= self.grid.y_coords.len() {
                return None;
            }
        }
        let res = Some((self.grid.x_coords[self.i], self.grid.y_coords[self.j]));
        self.i += 1;
        res
    }
}

fn main() {
    let grid = Grid { x_coords: vec![3, 5, 7, 9], y_coords: vec![10, 20, 30, 40] };
    for (x, y) in grid {
        println!("point = {x}, {y}");
    }
}
```

<details>

点击查阅 `IntoIterator` 文档。每个 `IntoIterator` 的实现都必须声明两种类型：

- `Item`：迭代的类型，例如 `i8`，
- `IntoIter`：`into_iter` 方法返回的 `Iterator` 类型。

注意 `IntoIter` 和 `Item` 是相连的：迭代器必须有相同的 `Item` 类型，意味着它返回 `Option<Item>`

例子中迭代了所有 x 和 y 坐标的组合。

尝试在 `main` 中对网格进行两次迭代。为什么会失败？注意 `IntoIterator::into_iter` 会取得 `self` 的所有权。

通过为 `&Grid` 实现 `IntoIterator` 并在 `GridIter` 中存储对 `Grid` 的引用来解决这个问题。

对于标准库类型也可能出现同样的问题：`for e in some_vector` 会取得 `some_vector` 的所有权并迭代该向量中拥有的元素。

```markdown
vector。请使用 `for e in &some_vector` 来遍历 `some_vector` 中元素的引用。
```
