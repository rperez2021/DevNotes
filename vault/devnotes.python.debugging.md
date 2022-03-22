---
id: cd1cg9uf5is0w7vq6v5nkfx
title: Debugging
desc: 'Notes on Python Debugging'
updated: 1647902617659
created: 1647902430948
---
## Using the Logging Module

```python
import logging
logging.basicConfig(level=logging.DEBUG, format=' %(asctime)s - %(levelname)s- %(message)s')
```

### Log Levels

- debug(lowest)
- info
- warning
- error
- critical(highest)
