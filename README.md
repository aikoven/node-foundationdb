# FoundationDB NodeJS bindings

These bindings are currently in the process of being revived and renewed from some very old code.

This is not yet production ready. The APIs will drift slightly over the next few weeks. But please give it a try and file issues against anything that isn't working yet.

## Usage

**You need to have the FDB client library on your machine before you can use this node module**. This is also true on any machines you deploy to. I'm sorry about that. We've been [discussing it](https://github.com/apple/foundationdb/issues/129).

#### Step 1

[Download a copy of foundationdb](https://www.foundationdb.org/download/)

#### Step 2

```
npm install --save foundationdb
```

#### Step 3

```javascript
const fdb = require('foundationdb')
// or  import fdb from 'foundationdb'

const db = fdb.openSync('fdb.cluster') // or just openSync() if the database is local.

db.transact(async tn => {
  console.log('key hi has value', await tn.getStr('hi'))
  tn.set('hi', 'yo')
})
```

The bindings currently support all the standard KV operations except range reads. They should be added over the next week or so.

The bindings do not currently support the `Directory` and `Tuple` layers. We have code, it just hasn't been ported to typescript. If someone wants to take a stab at it, raise an issue so we don't repeat work.

## Revival progress

- [x] Get it building on modern node / v8
- [x] Make all transaction primitives support promises
- [x] Native code works
- [x] Core rewritten in TS
- [x] Primitive transactions working from node
- [x] Transaction retry loop working
- [ ] Documentation
- [ ] Basic read range support
- [ ] Read range callback iterator support
- [ ] Read range async iterator
- [ ] Figure out a decent way to bundle the native `libfdb_c` code so users don't need to download their own copy
- [ ] Tuple support
- [ ] Directory support
- [ ] Basic local testing
- [ ] Testing integrated with the harness for the other bindings
- [ ] Add leveldown compatibilty
- [ ] Cut 1.0


## History

These bindings are currently based on an old version of FDB's bindings from years ago. The plan is to resurrect them over the next few weeks and get them production ready.

Patches welcome!