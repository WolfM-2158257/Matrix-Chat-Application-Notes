# Code convention
## Casing
### Klassen
Pascal Casing -> duidelijk voor modules
```kt
class PascalCasing {
	fun ThisIsPascalCasing
}
```
### variabelen & functies
in kotlin is het de standaard om private variabelen te definieren met een _{naam}.
daarnaast is het ook beter om Camel casing te gebruiken.
```kt
private var _camelCase?: Unit = null;
var isActive: Boolean = true;
```