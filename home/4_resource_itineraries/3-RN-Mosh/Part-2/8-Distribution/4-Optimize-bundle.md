# 4. Optimize bundle
Created Sat Dec 30, 2023 at 1:56 PM

1. **Lightweight packages** - try to use lighter libraries instead of heavier packages if possible. This is usually a geat optimization since many libraries are very powerful, but we use only a small portion of it. A simpler library may do the same thing.
2. **Submodules** - Sometimes, how we import also matters. Many libraries export submodules, and at the same time a default module that redundantly has the same function. Using the submodules approach here could help a lot. i.e. `import. { uniqueId } from lodash` is heavier than `import uniqueId from lodash/uniqueId`;