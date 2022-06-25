# 141. Managing cart and modal state
Created Saturday 25 June 2022

Modals generally have two components:
1. The content box
2. The backdrop - meaning the space surrounding the content box.

Usually, the content box has a "Cancel" button. Also, it's a good UX practice to make the backdrop clickable and the click to act as the "Cancel" button.

To have these features in a modal, make the modal consisting of two pieces, a backdrop `div` along with a "content box" placed at the centre. Add an `onClick` to the `div` (the backdrop) too.