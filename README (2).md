# Dart OOP Assignment: Kigali Bus Card

**Name:** Moumen Full Name

**Student ID:** 24429

## My numbers

- D = 29, L = 9
- Starting balance = 1000 + (29 x 10) = 1290 RWF
- Bus fare = 200 + 29 = 229 RWF
- Student discount = 10 + 9 = 19%

## Output of main.dart

```
Error: name too short
Owner: Moumen | Balance: 1290 RWF
Owner: Moumen Full Name | Balance: 1290 RWF
Error: top-up must be 500 to 50000 RWF
Topped up 2000 RWF
Paid 229 RWF
Paid 229 RWF
Owner: Moumen Full Name | Balance: 2832 RWF
Student discount: 43 RWF
Paid 186 RWF
Owner: Moumen Full Name | Balance: 1104 RWF
Student card: 19% off
```

## Part 1: Why no setter for balance?

If balance had a setter, any code could write any number into it, for example `card.balance = 999999`, and skip the rules. Without a setter, the balance can only change through `topUp` (which checks the 500 to 50000 limit) and `pay` (which refuses a fare bigger than the balance). So the money on the card stays safe and correct.

## Part 2: What does ~/ do?

`/` is normal division and gives a double (a number with decimals). `~/` is integer division: it divides and then drops the decimal part.

```
print(237 * 17 / 100);   // 40.29
print(237 * 17 ~/ 100);  // 40
```

In the student discount, `fare * _discount ~/ 100` gives a whole number of RWF.

## Part 4: Bug table

<table>
<tr><th>Bug</th><th>The line</th><th>Why it is wrong (your words)</th><th>Your fix</th></tr>
<tr><td>1</td><td><code>String _brand;</code></td><td>A String field needs a starting value, because Dart does not allow null here.</td><td><code>String _brand = '';</code></td></tr>
<tr><td>2</td><td><code>int _battery;</code></td><td>An int field also needs a starting value.</td><td><code>int _battery = 0;</code></td></tr>
<tr><td>3</td><td><code>SmartPhone(String brand, int battery, String system) {</code></td><td>The constructor does not call the parent constructor.</td><td>Add <code>: super(brand, battery)</code></td></tr>
<tr><td>4</td><td><code>@override void restart() {</code></td><td>The parent Phone has no restart method to override.</td><td>Remove <code>@override</code></td></tr>
<tr><td>5</td><td><code>print(p.battery());</code></td><td>battery is a getter, so it must not have parentheses.</td><td><code>print(p.battery);</code></td></tr>
<tr><td>Not a bug</td><td><code>Phone p = new Phone('Tecno', 50);</code></td><td>The new keyword is optional in Dart, so this line works.</td><td>(none)</td></tr>
</table>

I also added a setter for battery (needed for `p.battery = 100;`). It accepts only 0 to 100:

```dart
set battery(int value) {
  if (value >= 0 && value <= 100) {
    _battery = value;
  }
}
```

The fixed program prints `100`.

## Part 5

My prediction:

The first bag: `add()` makes items 1, then `a.items = -5` is refused because -5 is less than 0, so it prints 1. The BigBag: each `add()` calls `super.add()` twice, so two calls give 4 items, then `b.items = b.items + 1` sets it to 5. It prints 1 and then 5.

Real output:

```
1
5
```

Was I right?

Yes, my prediction was right.
