# 奇淫巧计
------

解决导出文件名乱码：
```php
header("Content-Disposition: attachment;filename*=UTF-8''" . urlencode($filename));
```

解决导出UTF-8编码到CSV文件乱码：
```php
// 在任何内容输出前先输出BOM
echo chr(0xEF).chr(0xBB).chr(0xBF);

/**
*
*为了识别 Unicode 文件，Microsoft 建议所有的 Unicode 文件应该以 ZERO WIDTH NOBREAK SPACE字符开头。这作为一个”特征符”或”字节顺序标记（byte-order mark，BOM）”来识别文件中使用的编码和字节顺序（big-endian或little-endian），具体的对应关系见下表。
*
*Bytes Encoding Form
*00 00 FE FF UTF-32, big-endian
*FF FE 00 00 UTF-32, little-endian
*FE FF UTF-16, big-endian
*FF FE UTF-16, little-endian
*EF BB BF UTF-8
*
*以UTF-8无BOM格式编码，因此要想导出Microsoft Excel可以正常显示的UTF-8的CSV文件，需要显式的输出BOM(EF BB BF，上表的最后一种类型)，然后再输出有效数据。
**/

```
