# utxompt
UTXO Set in a Merkle Patricia Trie

Use Rusty's bitcoin-iterate to generate text records and process:

    /usr/local/src/bitcoin-iterate/bitcoin-iterate \
        --quiet \
        --blockdir /mnt/t5/blocks \
        --input=I:%ih:%ii \
        --output=O:%th:%oN:%oa \
        | ./utxompt

