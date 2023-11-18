# 3. Shadows
Created Sun Nov 19, 2023 at 2:15 AM

This is platform specific. 
iOS is good, has many properties.
Android has just one property, and even that's not very effective.

## iOS
Have to apply at-least 3 properties:
- `shadowColor`
- `shadowOpacity`
- `shadowOffset: {{ width: 10, height: 10 }}` - decides size and position of shadows for the box. By default only right and bottom sides have shadow. Negative values will render shadow on the opposite side (left, and top).

More properties:
- `shadowRadius` - control blur. ~~rounding~~ (rounding is decided by original object, irrelevant).

## Android
As said, not much can be done.

The shadow here is a four sided one. So, not a true 2-side shadow. 
Color is fixed (black with low opacity).

Properties:
- `elevation: 10` - size of shadow

Changing the value doesn't do much, since a large number is essentially like background color.
Does not affect iOS.


[Code](https://github.com/exemplar-codes/DoneWithIt/commit/06f68e4d83a20bf9fd11c04ab5fb51525054de23)