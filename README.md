# To Run the Project

1. npm install
2. npm run dev

# API documentation

## List

```javascript
axios.get('/list')
```

## Delete

```javascript
axios.delete(`/del/${id}`)
```

## Edit

```javascript
axios.patch(`/edit/${id}`, {
  name: 'name',
  place: 'place of birth',
})
```
