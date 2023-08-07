# Java-Code-Snippets

## Arrays and Lists

Create `Stream<Integer>`
```
Arrays.stream(arr).boxed();
list.stream();
```

Create `Intstream`
```
Arrays.stream(arr);
list.stream().mapToInt(Integer::intValue);
```


### Maximum/minimum
```
intStream.max().orElse(Integer.MIN_VALUE);
intStream.min().orElse(Integer.MAX_VALUE);
```


### Convert To CountMap
For `arr = [1, 1, 3, 4, 4]` the Map would look like - `{1=2, 3=1, 4=2}` i.e. `count of 1 - 2. count of 3 - 1, count of 4 - 2`
```
stream.collect(Collectors.toMap(Function.identity(), v -> 1, (v1, v2) -> v1+v2));
```

### Convert to IndexMap
For `arr = [1, 1, 3, 4, 4]` the Map would look like - `{1=[0, 1], 3=[2], 4=[3, 4]}` i.e. `1 is present at indices [0,1]. 3 at [2] and 4 at [3,4]`

```
IntStream.range(0, arr.length).boxed().collect(Collectors.toMap(k -> arr[k], v -> {
    List<Integer> l = new ArrayList<>();
    l.add(v);
    return l;
}, (v1, v2) -> {
    v1.addAll(v2);
    return v1;
}));
```


## Maps

Merge 2 similar Maps (`map1` and `map2`). Here the Merging Functions adds the values of duplicate keys in the map.

If you want to do something else change `Integer::sum` to another function.
```
Stream.of(map1, map2)
  .flatMap(map -> map.entrySet().stream())
  .collect(Collectors.toMap(
              Map.Entry::getKey, Map.Entry::getValue, Integer::sum));
```

