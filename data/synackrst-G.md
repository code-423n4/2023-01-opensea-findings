## G-1: Use more efficient decrements in _validateOrdersAndPrepareToFulfill of OrderCombiner.sol

```
maximumFulfilled--;
```

can be rewritten as below to reduce the gas cost

```
---maximumFulfilled;
```

## G-2: Use more efficient increments in _getGeneratedOrder of OrderValidator.sol

```
contractNonce = _contractNonces[offerer]++;
```
can be rewritten as below to reduce the gas cost

```
contractNonce = ++_contractNonces[offerer];
```
