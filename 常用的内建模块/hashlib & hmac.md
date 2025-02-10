# hashlib

`hashlib` 是 Python 标准库中的一个模块，提供了一系列用于计算消息摘要（或称散列值）的函数。这些函数可以用来验证数据完整性、生成数字签名、存储密码等。



### hashlib模块中的主要函数和类

- `hashlib.md5([data])`：创建一个 MD5 哈希对象。
- `hashlib.sha1([data])`：创建一个 SHA-1 哈希对象。
- `hashlib.sha224([data])`：创建一个 SHA-224 哈希对象。
- `hashlib.sha256([data])`：创建一个 SHA-256 哈希对象。
- `hashlib.sha384([data])`：创建一个 SHA-384 哈希对象。
- `hashlib.sha512([data])`：创建一个 SHA-512 哈希对象。
- `hashlib.sha3_224([data])`：创建一个 SHA-3 224 哈希对象。
- `hashlib.sha3_256([data])`：创建一个 SHA-3 256 哈希对象。
- `hashlib.sha3_384([data])`：创建一个 SHA-3 384 哈希对象。
- `hashlib.sha3_512([data])`：创建一个 SHA-3 512 哈希对象。

### 使用示例

以下是一个基本的示例，展示了如何使用 `hashlib` 模块计算一个字符串的 SHA-256 哈希值：

```python
import hashlib

# 定义要哈希的字符串
string_to_hash = "Hello, World!"

# 创建一个 SHA-256 哈希对象
sha256_hash = hashlib.sha256()

# 将字符串编码为 bytes 并更新哈希对象
sha256_hash.update(string_to_hash.encode('utf-8'))

# 计算并打印哈ash 值
print(sha256_hash.hexdigest())
```

输出结果是一个长的十六进制字符串，表示输入字符串的 SHA-256 哈希值。

### 主要方法和参数解释

每个哈希对象都有以下主要方法：

- `update(data)`：更新哈希对象的状态，`data` 是要添加到哈希计算中的数据，必须是 bytes 类型。
- `digest()`：返回当前哈希对象的摘要（或称哈希值），以 bytes 形式返回。
- `hexdigest()`：返回当前哈希对象的摘要（或称哈希值），以十六进制字符串形式返回。
- `copy()`：返回当前哈希对象的副本。

在创建哈希对象时，可以传入一个可选的参数 `data`，它是要立即添加到哈希计算中的数据。例如：

```python
md5_hash = hashlib.md5(b"Hello, World!")
```

这将创建一个 MD5 哈希对象，并立即将字符串 "Hello, World!" 添加到哈希计算中。

### 注意事项

- 输入数据必须是 bytes 类型，否则会抛出 TypeError。
- 哈希函数是单向的，无法从哈希值反推出原始数据。
- 不同的哈希算法有不同的安全性和性能特性，应根据具体需求选择合适的算法。
- 在处理敏感数据（如密码）时，通常不直接使用哈希函数，而是使用专门的密码哈希函数（如 PBKDF2、bcrypt 等），以增加安全性。



# `hmac` 

 Python 标准库中的一个模块，提供了 HMAC（Hash-based Message Authentication Code，基于哈希的消息认证码）算法的实现。HMAC 用于验证消息的完整性和真实性，常用于数字签名和消息认证。

### hmac模块中的主要函数和类

- `hmac.new(key, msg=None, digestmod=None)`：创建一个新的 HMAC 对象。

### 使用示例

以下是一个基本的示例，展示了如何使用 `hmac` 模块生成一个 HMAC 签名：

```python
import hmac
import hashlib

# 定义密钥和消息
key = b'secret_key'
message = b'This is a secret message.'

# 创建一个新的 HMAC 对象，使用 SHA-256 作为哈希算法
hmac_obj = hmac.new(key, message, hashlib.sha256)

# 计算和打印 HMAC 签名
print(hmac_obj.hexdigest())
```

输出结果是一个十六进制字符串，表示输入消息的 HMAC 签名。

### 主要方法和参数解释

- ```
  hmac.new(key, msg=None, digestmod=None)
  ```

  ：

  - `key`：密钥，必须是 bytes 类型。
  - `msg`：消息，必须是 bytes 类型。如果在创建时不提供消息，可以在后续调用 `update()` 方法添加消息。
  - `digestmod`：哈希算法模块，默认是 hashlib.md5。可以选择其他哈希算法模块，例如 hashlib.sha256。

- `update(msg)`：更新 HMAC 对象的状态，`msg` 是要添加到 HMAC 计算中的消息，必须是 bytes 类型。

- `digest()`：返回当前 HMAC 对象的摘要（或称 HMAC 签名），以 bytes 形式返回。

- `hexdigest()`：返回当前 HMAC 对象的摘要（或称 HMAC 签名），以十六进制字符串形式返回。

- `copy()`：返回当前 HMAC 对象的副本。

### 注意事项

- 输入数据（密钥和消息）必须是 bytes 类型，否则会抛出 TypeError。
- 在选择哈希算法时，应考虑安全性和性能。SHA-256 是一个更安全的选择，而 MD5 可能不太安全。
- HMAC 签名是不可逆的，无法从签名中恢复出原始消息或密钥。
- 在实际应用中，密钥应该是保密的，并且不应与任何人共享。