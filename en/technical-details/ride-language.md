# RIDE Language for Waves Smart contracts

RIDE has no cycle and recursion possibility, unlike Solidity. We should note that RIDE as a language is not Turing-complete due to the lack of the possibility of creating loops or any other jump-like constructions.   
At the same time, it can be Turing-complete when used in conjunction with a blockchain, since theoretically the blockchain has an infinite length and we have other possibilities, e.g. DataTransaction.  
This kind of transaction provides data for smart contracts to work with. For example, if an oracle publishes some data once in a while using a publicly known account, smart contracts can use that data in their logic.  
Turing-completeness of a blockchain system can be achieved through unwinding the recursive calls between multiple transactions and blocks instead of using a single one, and it is not necessary to have loops and recursion in the language itself.

All constants are declared in lazy `let` constructions, which delays the evaluation of an expression until its value is needed, and does it at most once. For instance:

`let hash = blake2b256(preImage)`

The hash is not a variable: once created its values never change, and all structures are immutable.

`SetScriptTransaction` sets the script which verifies all outgoing transactions. The set script can be changed by another `SetScriptTransaction` call unless it’s prohibited by a previous set script.

There is a mechanism for checking a value against a pattern and you can handle the different expected types in a match expression. A match expression has a value, the match keyword, and at least one case clause:

```
match tx {
case t:Transfer =
>
 t.recepient
case t:MassTransfer =
>
 t.transfers
case _ =
>
 throw()
}
```

throw\(\) signals the occurrence of an exception during a script execution. In case of throw the transaction does not pass into the blockchain.
