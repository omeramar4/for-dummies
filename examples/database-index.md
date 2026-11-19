Unedited output of `/for-dummies what is a database index?` in a terminal.

---

**A database index is a separate, sorted lookup list that lets the database find rows fast without reading the whole table.**

## Analogy: the back-of-the-book index

Imagine a 500-page cookbook. You want every recipe with "basil."

- **No index:** you read all 500 pages. Slow.
- **With an index:** you flip to the back, find "basil: pages 42, 187, 301," and jump straight there.

| Book | Database |
|---|---|
| The book's pages | The table's rows |
| The back-of-book index | The database index |
| The word "basil" | The indexed column (e.g. `email`) |
| Page numbers | Pointers to where each row is stored |

Where it breaks: a book's index is printed once. A database index must be updated every time data changes.

## Example

A `users` table with 10 million rows:

```sql
SELECT * FROM users WHERE email = 'ana@example.com';
```

- **Without an index:** the database checks all 10,000,000 rows, one by one (a "full table scan").
- **With an index:**

```sql
CREATE INDEX idx_users_email ON users(email);
```

The database keeps emails in sorted order, in a tree structure. It jumps through about 3–4 levels of the tree, finds `ana@example.com`, and follows the pointer to the row. That's a handful of steps instead of 10 million.

```
          [ m ... ]                 <- start here
         /         \
   [ a ... f ]   [ n ... z ]        <- pick the right branch
      /    \
 [ana@..]  [bob@..]  -> pointer to the row on disk
```

## Common mix-up

Not "indexes make everything faster." They speed up **reads**, but cost **extra disk space** and make **writes slower**, because every insert, update, or delete must also update the index. Index the columns you search or sort by often, not every column.

## Why it matters

Without indexes, queries slow down as tables grow. With them, a search stays fast even with millions of rows.

## In short
- An index is a sorted shortcut list pointing to table rows.
- It turns "read everything" into "jump to the answer."
- Trade-off: faster reads, slower writes, more storage.

## Check yourself
Your table is written to constantly but rarely searched. Should you add many indexes?
*Answer: No. Each one slows every write, and you'd barely use them.*

*Level used: newcomer. Ask for "familiar" or "fluent" to go deeper.*
