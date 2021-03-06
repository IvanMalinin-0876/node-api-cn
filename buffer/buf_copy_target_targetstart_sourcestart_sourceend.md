<!-- YAML
added: v0.1.90
-->

* `target` {Buffer|Uint8Array} 要拷贝进的 `Buffer` 或 [`Uint8Array`]。
* `targetStart` {integer} `target` 中开始写入之前要跳过的字节数。**默认值:** `0`。
* `sourceStart` {integer} `buf` 中开始拷贝的偏移量。**默认值:** `0`。
* `sourceEnd` {integer} `buf` 中结束拷贝的偏移量（不包含）。**默认值:** [`buf.length`]。
* 返回: {integer} 拷贝的字节数。

拷贝 `buf` 中某个区域的数据到 `target` 中的某个区域，即使 `target` 的内存区域与 `buf` 的重叠。

[`TypedArray#set()`] 执行相同的操作，并且可用于所有的 TypedArray，包括 Node.js 的 Buffer，尽管它采用不同的函数参数。

```js
// 创建两个 `Buffer` 实例。
const buf1 = Buffer.allocUnsafe(26);
const buf2 = Buffer.allocUnsafe(26).fill('!');

for (let i = 0; i < 26; i++) {
  // 97 是 'a' 的十进制 ASCII 值。
  buf1[i] = i + 97;
}

// 拷贝 `buf1` 中第 16 至 19 字节偏移量的数据到 `buf2` 第 8 字节偏移量开始。
buf1.copy(buf2, 8, 16, 20);
// 这等效于：
// buf2.set(buf1.subarray(16, 20), 8);

console.log(buf2.toString('ascii', 0, 25));
// 打印: !!!!!!!!qrst!!!!!!!!!!!!!
```

```js
// 创建一个 `Buffer`，并拷贝同一 `Buffer` 中一个区域的数据到另一个重叠的区域。

const buf = Buffer.allocUnsafe(26);

for (let i = 0; i < 26; i++) {
  // 97 是 'a' 的十进制 ASCII 值。
  buf[i] = i + 97;
}

buf.copy(buf, 0, 4, 10);

console.log(buf.toString());
// 打印: efghijghijklmnopqrstuvwxyz
```

