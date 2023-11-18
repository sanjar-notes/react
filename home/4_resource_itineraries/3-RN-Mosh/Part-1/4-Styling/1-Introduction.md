# 1. Introduction
Created Sun Nov 19, 2023 at 1:55 AM

## `style` prop
- Most core components accept `style` prop, which is the only way to style stuff in RN
- The value of `style` is an object, or an instance of [`StyleSheet.create`](../2-Fundamental-concepts/8-StyleSheet.md)
- `style` can also be an array of objects, with the successive objects overriding previously mentioned properties, in a merge-with-replacement fashion.

## RN has no style inheritance
- Styles are not inherited in RN.
- Consequently, there's no need for specificity.

A common way to ensure consistency, especially for font styling, is to create wrappers for core RN components.

Commonly used style properties of the web are generally available in RN, at-least when it comes individual node styling.