# Blockchain

Demonstrate the easiest implement of blockchain concept

```javascript
const crypto = require('crypto')

const blockChains = []
function calcHash(data, preHash) {
    return crypto.createHmac('sha256', 'my secret')
        .update(data)
        .digest('hex');
}

function generateBlock({hash: preHash}, data) {
    return {
        data,
        hash: calcHash(data + preHash),
        preHash
    }
}

function verifyBlock(preBlock, block) {
    if (preBlock.hash !== block.preHash) {
        return false
    }

    if (calcHash(preBlock.hash + block.data) !== block.hash) {
        return false
    }

    return true
}

//Create blockchain
const firstBlock = generateBlock({ hash: 0 }, '我想藉由區塊練儲存的不可竄改資料')
blockChains.push(firstBlock)
blockChains.push(generateBlock(firstBlock, "新增的第二筆資料"))

//Create new block and save your data like this....
let lastBlock = blockChains[blockChains.length - 1]
blockChains.push(generateBlock(lastBlock, "新增的資料"))

//Use p2p module to sync blockchain
//blockchain slow because each node is creating block, it will conflict. 
//Resolve conflict called consensus, like voting 

```