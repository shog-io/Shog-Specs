# Messages

Shog is a message delivery protocol.

## Basic Message Format

```json
{
    "id": "string, keccak256 of message’s signature",
    "from": "string, shog id",
    "to": "string, shog id",
    "data": "string",
    "timestamp": "number, unix timestamp (in milliseconds)",
    "signature": "string, secp256k1 signature",
    "version": "string, protocol version",
    "type": "string, message type",
    "tags": {"name, string": "value, string or json"}
}
```

When no explicit to is specified, the target is "0000000000000000000000000000000000000000"

## Message Types

### Standard message

When to is specified, messages can be sent to an actor.
If encrypt is true, the data will be encrypted using the receiving actor's public key.

```json
{
    "to": "actor's shog id",
    "data": "message data",
    "type": "standard",
    "tags": {
        "encrypt": bool
    }
}
```

### Note

- CreateNote

a stand CreateNote message looks like: 

```json
{
    "to": "0000000000000000000000000000000000000000",
    "type": "createNote",
    "tags": {
            "mentions" : {
                "actor name": "shog id"
            }
        }
}
```

when reply to someone's note, it looks lik:

```json
{
    "data": "note data",
    "to": "actor's shog id",
    "type": "createNote",
    "tags": {
            "mentions" : {
                "actor name": "shog id"
            },
            "parent": "message id"
    }
}
```

- UpdateNote

```json
{
    "data": "updated data",
    "type": "updateNote",
    "tags": {
        "mentions" : {
                "actor name": "shog id"
        },
        "target": "need update note's message id"
    }
}
```

- DeleteNote

```json
{
    "type": "updateNote",
    "tags": {
        "target": "need delete note's message id"
    }
}
```

### Like

- likeNote

```json
{
    "to": "note's actor id",
    "type": "likeNote",
    "tags": {
        "target": "note's message id"
    }
}
```

- unlikeNote

```json
{
    "to": "note's actor id",
    "type": "unlikeNote",
    "tags": {
        "target": "note's message id"
    }
}
```

### Share

- shreNote

```json
{
    "to": "note's actor id",
    "type": "shareNote",
    "tags": {
        "target": "note's message id"
    }
}
```

- unshreNote

```json
{
    "to": "note's actor id",
    "type": "unshreNote",
    "tags": {
        "target": "note's message id"
    }
}
```
