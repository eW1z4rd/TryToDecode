## TryToDecode

> 属实是被各种编解码搞烦了，网上的在线工具复杂且不稳定，支持的编解码格式也乱七八糟，索性自己动手丰衣足食，一次解决所有烦恼🙃

TryToDecode，一款简单、快捷、准确的编解码工具，支持中文字符和特殊符号，**不需要任何第三方依赖，开箱即用**。可用于渗透测试和安全研究，也易于在项目中集成和二次开发。

目前支持的编解码方式有：

- url
- html
- base64
- unicode
- bin
- oct
- dec
- hex

如需支持更多编解码方式，欢迎补充 ^_^

### 使用说明 

初始化一个 `Convert` 对象，接收一个 str 或 bytes 类型的参数，自由调用并组合各种编解码方法，使用 `get()` 获取 str 类型的返回结果，使用 `get_bytes()` 获取 bytes 类型返回结果。

### 代码示例

```python
from lib.convert import Convert

s = '012abcABC!"#%&\'+中文字符'

if __name__ == '__main__':
    # hex编码
    print(Convert(s).str_to_hex().get())
    # \0x30\0x31\0x32\0x61\0x62\0x63\0x41\0x42\0x43\0x21\0x22\0x23\0x25\0x26\0x27\0x2b\0x4e2d\0x6587\0x5b57\0x7b26
    print(Convert(s).str_to_hex('&0x').get())  # 部分方法支持指定编解码时使用的分割符
    # &0x30&0x31&0x32&0x61&0x62&0x63&0x41&0x42&0x43&0x21&0x22&0x23&0x25&0x26&0x27&0x2b&0x4e2d&0x6587&0x5b57&0x7b26

    # 连续调用
    print(Convert(s).url_encode().str_to_base64().base64_to_str().url_decode().get())  # 012abcABC!"#%&'+中文字符

    # 三重base64编码
    for _ in range(3):
        s = Convert(s).str_to_base64().get()
    print(s)  # VFVSRmVWbFhTbXBSVlVwRVNWTkpha3BUV1c1TEsxTTBjbVZoVjJnclYzUnNLMlZ6Y0djOVBRPT0=
```