# production-project


```markdown
# Best Practices for Webpack Configuration

## Entry Path Configuration

### ✅ Good:
```js
const path = require('path');

module.exports = {
    entry: path.resolve(__dirname, 'src', 'index.js'),
};
```

### ❌ Bad:
```js
const path = require('path');

module.exports = {
    entry: './src/index.js',
};
```

### Почему лучше использовать `path.resolve`?
1. Гарантирует корректный абсолютный путь.
2. Избегает проблем с путями на Windows/Linux/macOS (прямой и обратный слэш).

---

## Output Configuration

### ✅ Good:
```js
output: {
    filename: '[name].[contenthash].js',
    path: path.resolve(__dirname, 'build'),
}
```

### ❌ Bad:
```js
output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'build'),
}
```

### Преимущества использования `[name].[contenthash].js`:
- `[name]` – вставляет имя точки входа (entry).
- `[contenthash]` – добавляет уникальный хеш, основанный на содержимом файла.

### Почему нельзя использовать просто `bundle.js`?
Если содержимое `bundle.js` изменится, браузер:
- закэширует старый файл;
- не заметит разницы, так как имя файла осталось прежним.

➡ Возможны проблемы с обновлением сайта у пользователей.
```
