## linux息屏
```
setterm -blank 1 -powersave powerdown 空闲 1 分钟后 让屏幕熄灭并进入省电状态
setterm -blank 0 -powersave off 恢复
```
## squaretest插件
 Squaretest 插件适用于 IntelliJ IDEA ，自动为您的 Java 类生成单元测试。

## 生成公钥和签名
```java
@RunWith(JUnit4.class)
public class Test {

	/** license
     --- BEGIN SQUARETEST LICENSE ---
     SQT1-AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
     SQT1-AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
     SQT1-AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
     将打印出的签名替换到此处
     --- END SQUARETEST LICENSE ---
     */
    @org.junit.Test
    @SneakyThrows
    public void testTimeOffset() {
        KeyPairGenerator keyPairGenerator = KeyPairGenerator.getInstance("DSA");
        KeyPair keys = keyPairGenerator.generateKeyPair();
        PublicKey publicKey = keys.getPublic();
        System.out.printf("pub:"+Base64.getEncoder().encodeToString(publicKey.getEncoded()));
        PrivateKey privateKey = keys.getPrivate();
        System.out.println("\n");
        System.out.println("priv:"+Base64.getEncoder().encodeToString(privateKey.getEncoded()));
        Signature sig = Signature.getInstance("SHA256withDSA", "SUN");

        sig.initSign(privateKey);

        String clearText = "SQT1-AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\n" +

                "SQT1-AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\n" +

                "SQT1-AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\n";

        sig.update(clearText.getBytes(StandardCharsets.UTF_8));

        byte[] signature = sig.sign();

        System.out.println("sign:"+Base64.getEncoder().encodeToString(signature));


        sig.initVerify(publicKey);

        sig.update(clearText.getBytes(StandardCharsets.UTF_8));

        boolean verify = sig.verify(signature);

        System.out.println("verify:"+verify);
    }
}

```


## 替换公钥
安装jclasslib插件后，找到squaretest插件的jar，一般在`user\AppData\Roaming\JetBrains\IntelliJIdea2022.2\plugins\Squaretest\lib`。启动java项目，将jar加载到libraries中。在external libraries中找到jar包，打开 `com.squaretest.c.q`这个类，替换公钥后保存。保存后替换原目录的jar，重启后填入license。
![a3c41c571a5c4cc5ad944223a9509e63](https://github.com/PICKNICK1/some-guide/assets/33755177/7687931d-feb0-4159-b047-d9a91eacfad0)
![860550f542244bfdb754e6a4e0346ef4](https://github.com/PICKNICK1/some-guide/assets/33755177/c04c01df-1808-4eda-aed5-277702170a8f)
![58e553d80c7e44478af4065e558d5cda](https://github.com/PICKNICK1/some-guide/assets/33755177/8a2761f9-ef2b-45c3-99b6-f14d8055820f)


## 实现原理：
请参考原文章。

>原文章信息: 
原作者：vycz
原出处：[https://www.cnblogs.com/vycz/p/15815842.html](https://www.cnblogs.com/vycz/p/15815842.html)
本作品采用<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">知识共享署名-非商业性使用-相同方式共享 4.0 国际许可协议</a>进行许可。
