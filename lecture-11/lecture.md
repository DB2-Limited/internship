# Lecture 11

### Fixtures

> https://github.com/powmedia/pow-mongodb-fixtures


### Plugins

> https://github.com/matteodelabre/mongoose-beautiful-unique-validation

###  Mongoose populate references

```js
.populate({
  path: 'example',
  select: 'field1 -field2'
})
```

### Mongoose queries

- `.limit()`
- `.skip()`
- `.sort()`
- `.select()`
- `$in`
- `$gt`
- `$lt`
- `$or`

### Error handling middleware

```js
module.exports = async (ctx, next) => {
  try {
    await next();
  } catch (err) {
    console.log(err);
    ctx.status = 500;
    ctx.body = {
      error: true,
    };
  }
}
```