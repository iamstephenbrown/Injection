# Injection

### What is it?

A base level package that allows us to use a property wrapper for dependency 

### How do I use it?

1. Extend InjectedValues and add your dependency, then create a struct to provide it

```
extension InjectedValues {
    var characterRepository: CharacterRepositoryInterface {
        get { Self[CharacterRepositoryServiceKey.self] }
        set { Self[CharacterRepositoryServiceKey.self] = newValue }
    }
}

private struct CharacterRepositoryServiceKey: InjectionKey {
    static var currentValue: CharacterRepositoryInterface = CharacterRepository()
}

```

2. Inject the dependency into your class

```
    @Injected(\.characterRepository) var characterRepository: CharacterRepositoryInterface
```

3. Replace the dependency in your tests or in your code. It will replace for all as it is a `static var`.

```
    InjectedValues[\.characterRepository] = MockCharacterRepository()
```

### Where did I steal it from?

This was shamelessly stolen from https://www.avanderlee.com/swift/dependency-injection/
