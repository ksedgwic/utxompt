# utxompt
UTXO Set in a Merkle Patricia Trie


#### levelpy

    git clone git@github.com:akubera/levelpy.git

```
diff --git a/levelpy/serializer.py b/levelpy/serializer.py
index 721a429..4a92b81 100644
--- a/levelpy/serializer.py
+++ b/levelpy/serializer.py
@@ -34,6 +34,14 @@ def binary_decode(byte_str):
     return byte_str
 
 
+def bytes_encode(byte_str):
+    return bytes(byte_str)
+
+
+def bytes_decode(byte_str):
+    return bytes(byte_str)
+
+
 class MsgPackSerializer:
 
     def __init__(self):
@@ -58,6 +66,7 @@ class Serializer:
         'utf-8': (utf8_encode, utf8_decode),
         'bin': (binary_encode, binary_decode),
         'binary': (binary_encode, binary_decode),
+        'bytes': (bytes_encode, bytes_decode),
         'none': (binary_encode, binary_decode),
         'msgpack': (MsgPackSerializer.encode, MsgPackSerializer.decode)
     }
```

#### Loading the DB

Use Rusty's bitcoin-iterate to generate text records and process:

    /usr/local/src/bitcoin-iterate/bitcoin-iterate \
        --quiet \
        --blockdir /mnt/t5/blocks \
        --block=B:%bN \
        --input=I:%ih:%ii \
        --output=O:%th:%oN:%oa \
        | ./load | tee output.log
        
The loader will create a list of root block hashes in `roots.txt`.

#### Generate a proof

The proof generator takes root_hash, txid and index as args:

    ./prove \
        6c079c9cfbc0d3dfe9f7133adb69ce8a555bb7641e4e3d988f19b0228e8f4640 \
        7e55be4820c159fd990893c8508e063bc5fe142d49ccca604647078c2c9305a7 \
        0 > proof.txt
        
#### Verify a proof

    ./verify \
        6c079c9cfbc0d3dfe9f7133adb69ce8a555bb7641e4e3d988f19b0228e8f4640 \
        7e55be4820c159fd990893c8508e063bc5fe142d49ccca604647078c2c9305a7 \
        0
