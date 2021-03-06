% Перечисления

В Rust есть "типы-суммы", или *перечисления* (тип-сумма - это термин из теории
типов). Перечисления - это очень полезная возможность Rust, и они очень много
используются в стандартной библиотеке языка. Они объявляются с помощью ключевого
слова `enum`. `enum` - это тип, который соотносит набор неких вариантов одному
имени. Например, ниже мы определяем перечисление `Character` (символ),
представляющее собой или цифру (`Digit`), или что-то другое.

```rust
enum Character {
    Digit(i32),
    Other,
}
```

Большая часть обычных типов могут быть вариантами перечисления. Вот несколько
примеров:

```rust
struct Empty;
struct Color(i32, i32, i32);
struct Length(i32);
struct Stats { Health: i32, Mana: i32, Attack: i32, Defense: i32 }
struct HeightDatabase(Vec<i32>);
```

Здесь мы видим, что, в зависимости от типа, вариант перечисления может
содержать, а может и не содержать вложенные данные. Например, в перечислении
`Character`, вариант `Digit` даёт значимое имя числу типа `i32`. А вот вариант
`Other` представляет собой лишь имя, без значения. Однако наиболее полезно
именно то, что отдельные варианты представляют собой различные виды символов
(`Character`).

Как и структуры, варианты перечислений по умолчанию не сравнимы операциями
сравнения (`==`, `!=`), не упорядочены (не реализуют `<`, `>=` и другие) и не
поддерживают другие двухместные операции, такие как умножение (`*`) и сложение
(`+`). Нижеследующий код, как таковой, не верен (если мы используем приведённый
выше тип-перечисление `Character`):

```rust,ignore
// Оба этих присваивания успешны
let ten  = Character::Digit(10);
let four = Character::Digit(4);

// Error: `*` is not implemented for type `Character`
let forty = ten * four;

// Error: `<=` is not implemented for type `Character`
let four_is_smaller = four <= ten;

// Error: `==` is not implemented for type `Character`
let four_equals_ten = four == ten;
```

Мы используем `::` синтаксис чтобы использовать имя каждого из вариантов. Их
область видимости ограничена именем самого перечисления `enum`. Это позволяет
использовать оба варианта из примера ниже совместно:

```rust,ignore
Character::Digit(10);
Hand::Digit;
```

Оба варианта имеют одинаковые имена, `Digit`, но область видимости каждого из
них ограничена соответствующим именем `enum`.

То, что эти операции не поддерживаются, может показаться достаточно
ограничивающим, но это ограничение, которое мы всегда можем преодолеть. Есть два
способа: посредством реализация равенства самостоятельно, или посредством
сопоставления вариантов с шаблонами с помощью выражений конструкции
[`match`][match], о котором вы узнаете в следующем разделе. Пока мы еще не знаем
достаточно о Rust для реализации равенства, но мы узнаем об этом в разделе
[`traits`][traits].

[match]: match.html
[traits]: traits.html
