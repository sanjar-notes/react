# 2. Rules
Created Sat Dec 30, 2023 at 1:33 PM

1. Navigation nature is guaranteed only within the navigator.
2. Each navigator must be a component, the name of this component will be the name (string) of the navigator.
3. Each child of navigator has to be a screen. If a child is a navigator, it will be registered as a screen with component prop being the nested navigator component.
4. Groups are meant for concise coding of header variations. If Groups construct didn't exist, mere difference of header would have necessitated the need to create a new navigator, and code for navigation would be cumbersome, even though the screens are semantically related but just differ in the header.
5. A navigator specifies header for all* screens under it. * meaning all direct (since groups are possible).
6. `options` callback prop on <Screen /> or <Group /> have the same value as if it were inside a Screen. What this means - that headerUI is semantically meant to be a component inside the screen. *This rule holds for other navigators too*
7. Navigator level header setting are actually an after thought, and are used if all screens have the same styling.
