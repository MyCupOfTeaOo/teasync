# teasync

该库主要是为了解决微服务场景下不同服务冗余外联字段导致的非关联键字段修改后数据处于非同步状态的问题

```sql
table home {
  id varchar(32),
  parent_id varchar(32),
  parent_name varchar(32),
  address varchar(64),
}
table person {
  id varchar(32),
  name varchar(32),
}
```

```js
const person = {
  id: 123,
  name: "嘎嘎嘎"
};
const home = {
  id: uuid,
  parent_id: 123,
  parent_name: "嘎嘎嘎",
  address: "未知地址"
};

// person.name "嘎嘎嘎" -> "啊啊啊"
person.name = "啊啊啊";
// but home.parent_name "嘎嘎嘎"
assert person.id === home.parent_id
assert person.name !== home.parent_name
```

这个时候就需要把 name 给同步过去

## todo

- [ ] 同步日志
- [ ] 定时同步
- [ ] 实时同步
- [ ] 适配 MySQL
- [ ] 适配 PostgreSQL
