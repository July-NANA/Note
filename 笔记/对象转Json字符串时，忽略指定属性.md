# 对象转Json字符串时，忽略指定属性

参考文档：[对象转Json字符串时，忽略指定属性]( https://blog.csdn.net/a491857321/article/details/78761857)

## JackSon忽略字段

@JsonIgnoreProperties({"字段1名","字段2名"}) 或者在字段上使用@JsonIgnore

```java
package com.gomefinance.esign;
 
import com.alibaba.fastjson.annotation.JSONField;
import com.fasterxml.jackson.annotation.JsonIgnore;
import com.fasterxml.jackson.annotation.JsonIgnoreProperties;
import lombok.Getter;
import lombok.Setter;
 
import java.io.Serializable;
 
/**
 * 本地签署信息
 * Created by JHAO on 2017/5/31.
 */
@Setter
@Getter
@JsonIgnoreProperties({"contractTemplateId", "contractImage"})
public class JackSonInputBean implements Serializable {
 
    // 合同模板ID
 
    private String contractTemplateId;
    // 合同号
    @JsonIgnore
    private String contractId;
    // Base64编码的合同
    private String contractImage;
    private String contractVersion;
 
}
```



