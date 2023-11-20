# Vyper入门: 2. 数值类型

### Vyper 提供对两类变量类型的访问：
	1. 数值: 合约中变量的任何使用都将直接传递其值
	2. 引用: 合约中变量的任何使用都将传递对内存中地址的引用，而不是值存储在那里。

#### 本节中我们只介绍数值类型，引用类型将在第4节中详细介绍

## 数值类型
1. 布尔型
	- bool: true或false
2. 数字 - 整型
	- int128: 有符号128位整数
	- int256: 有符号256位整数
	- uint8: 无符号8位整数
	- uint256: 无符号256位整数
3. 数字 - 浮点数
	- decimal: 带符号的浮点数，精度为10位小数
4. 地址
	- address: 20字节的十六进制数，带有0x前导数字
5. 字节数组
	- bytes32: 32字节数组，通常用于储存256位keccak哈希值
	- Bytes[N]: 可变长字节数组，N是存储的最大字节数组的长度
6. 字符串
	- String[N]: 保存字母数字字符串的可变长度字符串字节数组，其中N是存储的最大字符串的长度

#### 接下来介绍几个常用的数值类型

### 1. 布尔型
#### 布尔值分为 `True` 和 `False`, 布尔值的运算和Python一致。

#### 在Vyper中使用 `bool` 对变量进行声明，值默认为 `False`

```
is_bool: public(bool)

@payable
@external
def __init__():
	self.is_bool = True
```

#### 布尔值的运算包括
- not x: 逻辑非
- x and y: 逻辑与
- x or y: 逻辑或
- x == y: 等于
- x != y: 不等于

#### 代码示例：
```
bool1: bool = True
bool2: bool = not bool1

bool1 and bool2 -> False
bool1 or bool2 -> True
bool1 == bool2 -> False
bool1 != bool2 -> True

```

### 2. 整型
#### 常用的整型包括
```
# 有符号的256位整数，包括负数
number: int256 = -1

# 无符号的256位正整数
number: uint256 = 123456
```

#### 整型运算包括
	- 比较运算符（返回布尔值）： `==`, `!=`, `<`, `>`, `<=`, `>=`
	- 算术运算符: `+`, `-`, `*`, `/`, `**`, `%`
	- 按位运算符：`&`, `|`, `^`

#### Vyper中，只有相同类型的变量才能进行运算
#### 代码示例：
```
x: uint256 = 100
y: uint256 = 200

is_bool: bool = x < y
number: uint256 = x + y
number2: uint256 = x & y
```

### 3. 地址
#### Vyper中的地址类型是一种基本的数据类型，用于存储一个20字节的以太坊地址，这些地址通常包括外部账户和合约账户
#### 在Vyper中直接使用 `address` 关键字声明
```
owner: public(address)

self.owner = 0xEeeeeEeeeEeEeeEeEeEeeEEEeeeeEeeeeeeeEEeE
```

### 4. 字节数组
#### 在Vyper中，字节数组是用于存储和处理字节序列的数据类型，具体分为定长字节数组(bytesN)和可变字节数组(Bytes[N])
#### **bytesN**
#### `bytesN` 这是一个 `N` 字节宽的字节数组, 比如 `bytes32` 是一个固定长度的32字节的字节数组。它通常用于存储256位的keccak哈希值、密钥和其他固定长度的加密数据。`bytes4`常用于存储函数方法

#### 代码示例
```
# 0x4f8b61438cf1d5e6f4f684d62bf496fc8975999b940392b49a2b70e209a69c12
bytes_value: bytes32 = keccak256("Vyper")

method: bytes4 = 0x01abcdef
```

#### **Bytes[N]**
#### `Bytes[N]` 是一个可变长度的字节数组，其中 `N` 定义了字节数组的最大长度。

#### 代码示例
```
bytes_string: Bytes[100] = b"\x01"
```

### 5. 字符串
#### `String[N]` 是一个可变长度的字符串字节数组，其中 `N` 定义了字符串的最大长度。它是专门用于存储文本数据的类型，与Bytes[N]类似，但更适合处理纯文本。

#### 代码示例
```
example_str: String[100] = "Hello Vyper!"
```

## 总结
#### 在本节中，我们介绍了 `Vyper` 中的5种变量类型，如果想要了解更加详细的类型内容，可以在[官方文档](https://docs.vyperlang.org/en/latest/types.html)中查看。