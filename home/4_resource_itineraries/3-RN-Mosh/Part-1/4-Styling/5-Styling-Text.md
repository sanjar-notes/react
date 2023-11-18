# 5. Styling Text
Created Sun Nov 19, 2023 at 3:17 AM

## Style props
- `color` string. Examples: `'red'`,  `'#ff0000'`
- `fontWeight` - string. Examples: `'600'`, `'bold'`, `'normal'`. JS number won't work.
- `fontSize` - number
- `fontFamily`

Note: these work with `Text` only. They won't have any effect if used on `View` etc.

## Font family
iOS and Android have no common system fonts. So using `Platform` is non-optional.

```jsx
<Text styles={{ 
  fontFamily: Platform.OS === 'android' ? 'Roboto': 'Arial'
}}>
  Hello world
</Text>
```

Fonts:
- Android - "normal" (aka "Roboto"), "serif", "monospace"
- iOS - "Helvetica", "Georgia", "Times New Roman"

Fallbacks are not supported.

## More style props
- `textTransform` - `'capitalize'`, `'uppercase'`, `'lowercase'`
- `textDecorationLine` - `'underline'`, `'line-through'`
- `textAlign` - `'left'`, `'right'`, `'justify'`
- `lineHeight` - number. Used to change space between lines of a paragraph.

## Consistent text tip
Since RN has no style inheritance, showing text consistently across the app is difficult if done via props (inline or via shared/global/external styles) - would be too much work, be anti-DRY and forgetful.

The solution is simple - create a wrapper that uses `<Text />` and prohibit direct usage of `<Text />`. This wrapper component can have the styles we want already set as default props.

In fact, most RN project devs create wrappers for most components, when:
1. Styling needs to be consistent
2. Cross-platform issues exist. This avoids using Platform API in the feature code (which is good)