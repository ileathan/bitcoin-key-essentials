# bitcoin-key-essentials
the minimal needed i believe.
```javascript
const crypto = require('crypto');
const eccrypto  = require('eccrypto')

const t = _ => _.toString('hex')
const r = _ => !(_.compare((new Buffer('0000000000000000000000000000000000000000000000000000000000000001', 'hex'))) < 0)
      && !(_.compare((new Buffer('FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFEBAAEDCE6AF48A03BBFD25E8CD0364140', 'hex'))) > 0)
         ? _
    : r(crypto.randomBytes(32)) ;

privateKey = r(crypto.randomBytes(32))
// OR privateKey = new Buffer(YOUR_KEY, 'hex')

const publicKey = eccrypto.getPublic(privateKey)
var hash      = crypto.createHash('sha256').update(publicKey).digest()
hash      = crypto.createHash('ripemd160').update(hash).digest()
var checksum  = Buffer.concat([(version = new Buffer('00', 'hex')), hash])
checksum  = crypto.createHash('sha256').update(checksum).digest()
checksum  = crypto.createHash('sha256').update(checksum).digest().slice(0,4)
const address   = require('bs58').encode(Buffer.concat([version, hash, checksum]))

console.log(address) // Send money here
console.log(privateKey) // Claim money here

//console.log([t(privateKey), t(hash), t(version), t(checksum), t(address), t(publicKey)])

//EC = require("elliptic").ec;
//ec = new EC("secp256k1");
//shaMsg = crypto.createHash("sha256").update("leathan").digest();
//mySign = ec.sign(shaMsg, privateKey, {canonical: true});
//console.log(shaMsg, privateKey)
//console.log(mySign)
```
