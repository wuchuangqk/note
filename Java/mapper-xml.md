# 头部
```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.lan.maid.mapper.ClothesMapper">
</mapper>
```


# select

```xml
<select id="getIdleClothes" resultType="Clothes">
  select clothes.* from clothes
  left join maid_clothes
  on maid_clothes.clothes_id = clothes.id
  <where>
    <if test="kind != null">
      and clothes.kind = #{kind}
    </if>
    and maid_clothes.id is null
  </where>
</select>
```



# insert

```xml
<insert id="addRelation">
  insert into maid_clothes(maid_role, clothes_id, wear_time)
  VALUES (#{maidRole}, #{clothesId}, #{wearTime});
</insert>
```



# update

```xml
<update id="updateClothesStatus">
  update clothes set is_clean = #{status} where id = #{id};
</update>
```



# delete

```xml
<delete id="removeRelation">
  delete from maid_clothes where id = #{id}
</delete>
```



# resultMap

```xml
<resultMap id="MaidClothesMap" type="MaidClothes">
  <id property="id" column="mc_id" />
  <association property="clothes">
    <id property="id" column="id" />
  </association>
</resultMap>
```

