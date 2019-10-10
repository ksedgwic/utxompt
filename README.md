# utxompt
UTXO Set in a Merkle Patricia Trie


#### Merkle-Patricia-Trie

    git clone git@github.com:lovesh/Merkle-Patricia-Trie.git

```
diff --git a/storage/refcount_db.py b/storage/refcount_db.py
index 44e4f7c..2e4c64c 100644
--- a/storage/refcount_db.py
+++ b/storage/refcount_db.py
@@ -37,7 +37,7 @@ class RefcountDB:
             assert existing[4:] == value
             self.db.put(key, add1(existing[:4]) + value)
             # print('putin', key, utils.big_endian_to_int(existing[:4]) + 1)
-        except KeyError:
+        except (KeyError, TypeError):
             self.db.put(key, b'\x00\x00\x00\x01' + value)
             # print('putin', key, 1)
 
```

#### Running

Use Rusty's bitcoin-iterate to generate text records and process:

    /usr/local/src/bitcoin-iterate/bitcoin-iterate \
        --quiet \
        --blockdir /mnt/t5/blocks \
        --input=I:%ih:%ii \
        --output=O:%th:%oN:%oa \
        | ./utxompt

