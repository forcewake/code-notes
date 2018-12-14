---
title: Node.js
category: Typescript
order: 1
---

## How to get parent directory name in Node.js

```typescript
path.basename(path.dirname(file))
```

## How to get all files from directory and inner directories

```typescript
const layoutsFolder = './path/to/dir'

function* walkSync(dir: string): IterableIterator<string> {
  const files = fs.readdirSync(dir)
  for (const file of files) {
    const pathToFile = path.join(dir, file)
    const isDirectory = fs.statSync(pathToFile).isDirectory()
    if (isDirectory) {
      yield* walkSync(pathToFile)
    } else {
      yield pathToFile
    }
  }
}
```
