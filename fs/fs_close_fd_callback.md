<!-- YAML
added: v0.0.2
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/12562
    description: 参数 `callback` 不再是可选的。 
      如果不传入，则在运行时会抛出 `TypeError`。
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7897
    description: 参数 `callback` 不再是可选的。 
      如果不传入，则会触发弃用警告（id 为 DEP0013）。
-->

* `fd` {integer}
* `callback` {Function}
  * `err` {Error}

异步的 close(2)。
除了可能的异常，完成回调没有其他参数。

通过任何其他 `fs` 操作在当前正在使用的任何文件描述符（`fd`）上调用 `fs.close()` 可能导致未定义的行为。

