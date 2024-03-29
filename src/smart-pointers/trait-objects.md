---
minutes: 10
translated_at: '2024-03-26T10:13:11.427Z'
---

# 特征对象

特征对象允许不同类型的值，例如在集合中：

```rust,editable
struct Dog {
    name: String,
    age: i8,
}
struct Cat {
    lives: i8,
}

trait Pet {
    fn talk(&self) -> String;
}

impl Pet for Dog {
    fn talk(&self) -> String {
        format!("汪汪，我的名字是 {}！", self.name)
    }
}

impl Pet for Cat {
    fn talk(&self) -> String {
        String::from("喵！")
    }
}

fn main() {
    let pets: Vec<Box<dyn Pet>> = vec![
        Box::new(Cat { lives: 9 }),
        Box::new(Dog { name: String::from("Fido"), age: 5 }),
    ];
    for pet in pets {
        println!("你好，你是谁？{}", pet.talk());
    }
}
```

在分配 `pets` 后的内存布局：

```bob
 栈                                堆
.- - - - - - - - - - - - - - -.     .- - - - - - - - - - - - - - - - - - - - - -.
:                           :     :                                             :
:    "pets: Vec<dyn Pet>"   :     :   "data: Cat"         +----+----+----+----+ :
:   +-----------+-------+   :     :  +-------+-------+    | F  | i  | d  | o  | :
:   | ptr       |   o---+---+--.  :  | lives |     9 |    +----+----+----+----+ :
:   | len       |     2 |   :  |  :  +-------+-------+      ^                   :
:   | capacity  |     2 |   :  |  :       ^                 |                   :
:   +-----------+-------+   :  |  :       |                 '-------.           :
:                           :  |  :       |               data:"Dog"|           :
:                           :  |  :       |              +-------+--|-------+   :
`- - - - - - - - - - - - - -'  |  :   +---|-+-----+      | name  |  o, 4, 4 |   :
                               `--+-->| o o | o o-|----->| age   |        5 |   :
                                  :   +-|---+-|---+      +-------+----------+   :
                                  :     |     |                                 :
                                  `- - -| - - |- - - - - - - - - - - - - - - - -'
                                        |     |
                                        |     |                      "程序文本"
                                  .- - -| - - |- - - - - - - - - - - - - - - - -.
                                  :     |     |       vtable                    :
                                  :     |     |      +----------------------+   :
                                  :     |     `----->| "<Dog as Pet>::talk" |   :
                                  :     |            +----------------------+   :
                                  :     |             vtable                    :
                                  :     |            +----------------------+   :
                                  :     '----------->| "<Cat as Pet>::talk" |   :
                                  :                  +----------------------+   :
                                  :                                             :
                                  '- - - - - - - - - - - - - - - - - - - - - - -'
```

<details>

- 实现了特定 trait 的类型可能具有不同的大小。这使得像上面例子中的 `Vec<dyn Pet>` 这样的事情成为不可能。
- `dyn Pet` 是一种告诉编译器关于动态尺寸类型实现了 `Pet` 的方式。
- 在示例中，`pets` 被分配在栈上，向量数据位于堆上。这两个向量元素是 _胖指针_：
  - 胖指针是一个双宽度指针。它有两个组件：一个指向实际对象的指针和一个指向该特定对象的 `Pet` 实现的 [虚方法表] （vtable）的指针。
  - 名为 Fido 的 `Dog` 的数据是 `name` 和 `age` 字段。`Cat` 有一个 `lives` 字段。
- 比较上例中的这些输出：
  ```rust,ignore
  println!("{} {}", std::mem::size_of::<Dog>(), std::mem::size_of::<Cat>());
  println!("{} {}", std::mem::size_of::<&Dog>(), std::mem::size_of::<&Cat>());
  println!("{}", std::mem::size_of::<&dyn Pet>());
  println!("{}", std::mem::size_of::<Box<dyn Pet>>());
  ```

[虚方法表]: https://en.wikipedia.org/wiki/Virtual_method_table

</details>
