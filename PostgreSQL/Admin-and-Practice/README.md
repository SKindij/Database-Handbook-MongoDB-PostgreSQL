# Administration and Best Practices

## @vercel/postgres
_A client that works with Vercel Postgres._

#### Install
`npm install @vercel/postgres`

#### Importing
```typescript
// Don't need any custom config?:
import { sql } from '@vercel/postgres';
// `sql` is already set up and ready to go; no further action needed

// Need to customize your config?:
import { createPool } from '@vercel/postgres';
const pool = createPool({
  /* config */
});

// Need a single client?:
import { createClient } from '@vercel/postgres';
const client = createClient({
  /* config */
});
```






