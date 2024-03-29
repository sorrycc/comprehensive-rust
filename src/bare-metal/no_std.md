---
translated_at: '2024-03-26T11:31:34.438Z'
---

# `no_std`

<table>
<tr>
<th>

`core`

</th>
<th>

`alloc`

</th>
<th>

`std`

</th>
</tr>
<tr valign="top">
<td>

- 切片，`&str`，`CStr`
- `NonZeroU8`...
- `Option`，`Result`
- `Display`，`Debug`，`write!`...
- `Iterator`
- `panic!`，`assert_eq!`...
- `NonNull` 以及所有常用的指针相关函数
- `Future` 和 `async`/`await`
- `fence`，`AtomicBool`，`AtomicPtr`，`AtomicU32`...
- `Duration`

</td>
<td>

- `Box`，`Cow`，`Arc`，`Rc`
- `Vec`，`BinaryHeap`，`BtreeMap`，`LinkedList`，`VecDeque`
- `String`，`CString`，`format!`

</td>
<td>

- `Error`
- `HashMap`
- `Mutex`，`Condvar`，`Barrier`，`Once`，`RwLock`，`mpsc`
- `File` 及其他 `fs` 相关
- `println!`，`Read`，`Write`，`Stdin`，`Stdout` 及其他 `io` 相关
- `Path`，`OsString`
- `net`
- `Command`，`Child`，`ExitCode`
- `spawn`，`sleep` 及其他 `thread` 相关
- `SystemTime`，`Instant`

</td>
</tr>
</table>

<details>

- `HashMap` 依赖于 RNG。
- `std` 重新导出了 `core` 和 `alloc` 的内容。

</details>
