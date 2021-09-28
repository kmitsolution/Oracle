# TCL (Transcation Control Language)
1. Commit
2. Rollback
3. SET Transaction
4. Savepoint

## Example

```sql
COMMIT; 

SET TRANSACTION READ ONLY NAME 'Toronto'; 

SELECT product_id, quantity_on_hand FROM inventories
   WHERE warehouse_id = 5
   ORDER BY product_id; 

COMMIT; 
```
