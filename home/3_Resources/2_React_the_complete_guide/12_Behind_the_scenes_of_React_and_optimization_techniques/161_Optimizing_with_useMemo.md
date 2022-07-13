# 161. Optimizing with useMemo
Created Monday 11 July 2022

- `React.memo` diffs all props, in constrast, `useMemo` hook allows for selective diffing of props.
- `useMemo` is closer to `useCallback` that `React.memo`.
- `useMemo` is generally needed on both sender and receiver component.

![](drawing.drawio.svg)