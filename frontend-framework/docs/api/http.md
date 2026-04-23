# HTTP API

A unified wrapper around the browser's `fetch` API for making JSON requests.

## Methods

All methods return a Promise that resolves to the JSON response body. If the response status is not OK (200-299), an Error is thrown.

### `http.get(url, options)`
PERFORMS A GET REQUEST.

**Parameters:**
- `url` *(string)*: The endpoint URL.
- `options` *(object)*: Standard fetch options (headers, etc.).

**Returns:** `Promise<any>`

### `http.post(url, data, options)`
Performs a POST request with JSON body.

**Parameters:**
- `url` *(string)*: The endpoint URL.
- `data` *(object)*: The data to serialize as JSON.
- `options` *(object)*: fetch options.

### `http.put(url, data, options)`
Performs a PUT request with JSON body.

### `http.delete(url, options)`
Performs a DELETE request.

## Example

```javascript
import { http } from '../index.js';

async function loadData() {
    try {
        const user = await http.get('/api/user/1');
        await http.post('/api/log', { action: 'viewed_user', id: user.id });
    } catch (err) {
        console.error("Request failed", err);
    }
}
```
