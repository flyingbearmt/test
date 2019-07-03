== 如果是primitive number 比的是 内容
	如果是 对象，比的是地址 
	
.equal比的是内容

``` java
String aString = "hello";
String bString = "hello";
Integer aInteger = new Integer(4);
Integer bInteger = new Integer(4);
int a = 3;
int b = 3;
System.out.println(a==b);                  	//true
System.out.println(aInteger ==bInteger); 	//false
System.out.println(aString == bString); 	//true
System.out.println(aString.equals(bString)); 	//true
```



collection| get| put| change| delete| haveOrNot
----------|----|----|-----|------|-----
map| get/getOrDefault| put|replace(key,value)|remove|containsKey/containsValue

// Make a new empty map

Map<String, String> map = new HashMap<String, String>();

map.get(key) -- retrieves the stored value for a key, or null if that key is not present in the map.

map.put(key, value) -- stores a new key/value pair in the map. Overwrites any existing value for that key.

map.containsKey(key) -- returns true if the key is in the map, false otherwise.

map.remove(key) -- removes the key/value pair for this key if present. Does nothing if the key is not present.  

#### treemap
在treemap中还有几个方法：   
lowerEntry、floorEntry、ceilingEntry 和 higherEntry 分别返回与小于、小于等于、大于等于、大于给定键的键关联的 Map.Entry 对象，如果不存在这样的键，则返回 null。类似地，方法 lowerKey、floorKey、ceilingKey 和 higherKey 只返回关联的键。