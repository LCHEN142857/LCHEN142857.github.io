# Mybatis Tips

## 1. 配置新增项返回主键ID

```java
<insert id="addItem" userGenerateKeys="true" keyProperty="itemId" parameterType="Item">
itemMapper.addItem(item);
int itemId = item.getItemId(); // 此时的item就含有返回的主键ID
```

## 2. 一次插入多条数据

- 注意foreach标签会将空格，换行，回车等问题带入SQL语句中

```xml
<insert id="addSteps" parameterType="java.util.list">
    INSERT INTO `memo`.`step` (`seq_id`, `item_id`, `step_description`)
    VALUES
    <foreach collection="list" item="item" index="index" separator=",">
        (#{item.seqId},
        #{item.itemId},
        #{item.description})
    </foreach>
</insert>
```

## 3. 传入多个不同类型的参数

- eg: 一个父类（泛指上一级）实体的itemId，多个子类（泛指子级）的集合stepList，每个子类都有同样的itemId，就不用循环给参数赋值在传给mapper了

```java
int addSteps(@Param("stepList") List<Step> stepList, @Param("itemId") int itemId);
```

```xml
<insert id="addSteps" parameterType="java.util.list">
    INSERT INTO `memo`.`step` (`seq_id`, `item_id`, `step_name`)
    VALUES
    <!--stepList, itemId根据参数带入-->
    <foreach collection="stepList" item="item" index="index" separator=",">
        (#{item.seqId},
        #{itemId},
        #{item.stepName})
    </foreach>
</insert>
```

## 4. update-set语句

- set语句会产出一个set关键字，并去掉动态拼接的最后一个语句的逗号
