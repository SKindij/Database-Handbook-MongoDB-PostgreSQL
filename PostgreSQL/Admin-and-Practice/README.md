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




- - -

### Edge environments

It is a term commonly used in the context of deploying software or web applications. In the case of Vercel, it refers to different areas or locations where servers or execution environments for your application may be placed.

These environments are strategically positioned to bring the code closer to end-users, reducing response times (latency), and improving application performance. This allows for swift access to content for users across different parts of the world.

Typically, edge environments are deployed in various geographical locations such as different countries or regions to provide optimal performance for each user. This involves lifting parts or all of the application closer to end-users, reducing the distance between servers and users, and consequently decreasing response times.

In the context of Vercel, it may involve deploying your web application on various servers worldwide to ensure rapid access for users from different regions.

- - -





