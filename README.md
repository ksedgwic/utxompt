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

#### Running

Use Rusty's bitcoin-iterate to generate text records and process:

    /usr/local/src/bitcoin-iterate/bitcoin-iterate \
        --quiet \
        --blockdir /mnt/t5/blocks \
        --block=B:%bN \
        --input=I:%ih:%ii \
        --output=O:%th:%oN:%oa \
        | ./utxompt | tee output.log

