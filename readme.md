#
### 使用依赖
```
<dependency>
    <groupId>com.github.gitveio</groupId>
    <artifactId>gmssl-dev</artifactId>
    <version>1.0</version>
</dependency>
```

### 示例
```
GmSSL gmSSL = new GmSSL();

// SMS4加解密，替换des..
byte[] key = {1,2,3,4,5,6,7,8,1,2,3,4,5,6,7,8};
byte[] iv = {1,2,3,4,5,6,7,8,1,2,3,4,5,6,7,8};
byte[] s1 = gmSSL.symmetricEncrypt("SMS4", "1234566".getBytes(), key, iv);
byte[] s2 = gmSSL.symmetricDecrypt("SMS4", s1, key, iv);

// SM3哈希，替换md5/sha128...
byte[] s3 = gmSSL.digest("SM3", "adfd".getBytes());
for (int i = 0; i < s3.length; i++) {
    System.out.printf("%02X", s3[i]);
}
```

# windows编译
1 替换names2.c为老版本文件  
2 安装vs、activeperl、nasm  
3 打开visual studio 2015 -> x64 x86 cross ..  
4 切换至gmssl根目录，执行  
```
>> perl Configure VC-WIN64A no-asm
>> nmake
```
5 切换至java目录，执行  
```
>> nmake -f winmake
```

# linux编译
1 编辑Configure，添加"java"  
$config{dirs} = [ "crypto", "ssl", "engines", "apps", "util", "tools", "fuzz", "test", "java" ];  
2 删除报错的--verion..map段  
3 ./config  
4 make  