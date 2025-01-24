# Optional Containers in Java

Java provides several optional containers to handle values that may or may not be present. Here is a list of commonly used ones:

## 1. `Optional` (Java 8+)
- **Package**: `java.util`
- Represents a container object that may or may not contain a non-null value.
- Common Methods:
  - `empty()`: Returns an empty `Optional` instance.
  - `of(T value)`: Returns an `Optional` with the specified non-null value.
  - `ofNullable(T value)`: Returns an `Optional` with the specified value, or empty if `null`.
  - `isPresent()`: Checks if a value is present.
  - `ifPresent(Consumer<? super T> action)`: Executes the specified action if the value is present.
  - `orElse(T other)`: Returns the value if present, otherwise returns the specified default value.
  - `orElseGet(Supplier<? extends T> supplier)`: Returns the value if present, or uses the supplier to provide a default value.
  - `orElseThrow(Supplier<? extends X> exceptionSupplier)`: Throws an exception if no value is present.

## 2. `OptionalDouble`, `OptionalInt`, and `OptionalLong` (Java 8+)
- **Package**: `java.util`
- Primitive-specific versions of `Optional` for `double`, `int`, and `long`.
- Common Methods:
  - `isPresent()`: Checks if a value is present.
  - `getAsDouble()` / `getAsInt()` / `getAsLong()`: Returns the value if present.
  - `orElse(double/int/long other)`: Returns the value if present, otherwise returns the specified default.
  - `orElseThrow(Supplier<? extends X> exceptionSupplier)`: Throws an exception if no value is present.

## 3. `AtomicReference<T>` (Optional-like behavior for threads)
- **Package**: `java.util.concurrent.atomic`
- Acts as a thread-safe container for an object reference that can be updated atomically.
- Common Methods:
  - `get()`: Retrieves the current value.
  - `set(T newValue)`: Sets the value.
  - `compareAndSet(T expect, T update)`: Atomically sets the value if it matches the expected value.

## 4. `OptionalStage` (Custom Utility in Libraries)
- Libraries like **Vavr** or **Guava** extend Java's `Optional` capabilities.
  - **Guava**: Provides `Optional` in older versions for compatibility before Java 8.
  - **Vavr**: Provides a `io.vavr.control.Option` as a functional alternative.

## Use Cases of Optional Containers
- Avoid `null` references and reduce `NullPointerException` occurrences.
- Encapsulate optional values explicitly.
- Improve code readability and enforce handling of potential absence of values.

## Notes
- Using `Optional` for return types is recommended.
- Avoid using `Optional` for fields, method parameters, or collections due to potential performance overhead.

These containers are essential for writing robust and null-safe Java applications.
