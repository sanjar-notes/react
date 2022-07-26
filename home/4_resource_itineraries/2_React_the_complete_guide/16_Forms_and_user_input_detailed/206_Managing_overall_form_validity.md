# 206. Managing overall form validity
Created Tuesday 26 July 2022

*Nothing new here*.
- Have a single variable that stores the overall form validity. This is not generally a state variable, as it can be derived using other states/derived_states.
- This variable may be binary yes/no, or there could be multiple valid states of a form (for example, when some inputs are optional and therefore can be left empty).