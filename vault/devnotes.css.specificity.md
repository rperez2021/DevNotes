---
id: qf9443fygt5ex993crv5c0w
title: CSS Specificity
desc: 'CSS Specificty Notes'
updated: 1647319805546
created: 1647312641814
---
## Calculating CSS Specificity Value

- If the element has inline styling, that automatically1 wins (1,0,0,0 points)
- For each ID value, apply 0,1,0,0 points
- For each class value (or pseudo-class or attribute selector), apply 0,0,1,0 points
-For each element reference, apply 0,0,0,1 point

## Important Notes

- The universal selector (*) has no specificity value (0,0,0,0)
- Pseudo-elements (e.g. :first-line) get 0,0,0,1 unlike their psuedo-class brethren which get 0,0,1,0
- The pseudo-class :not() adds no specificity by itself, only what’s inside it’s parentheses.
- The !important value appended a CSS property value is an automatic win. It overrides even inline styles from the markup. The only way an !important value can be overridden is with another !important rule declared later in the CSS and with equal or great specificity value otherwise. You could think of it as adding 1,0,0,0,0 to the specificity value.

## Examples

![Specificity Explainer](assets\images\specificity_blank.webp){width: 300px}

![Specificity Example 1](assets\images\cssspecificity_ex1.webp){width: 300px}

![Specificity Example 2](assets\images\cssspecificity_ex2.webp){width: 300px}

![Specificity Example 3](assets\images\cssspecificity_ex3.webp){width: 300px}

![Specificity Example 4](assets\images\cssspecificity_ex4.webp){width: 300px}

![Specificity Example 5](assets\images\cssspecificity_ex5.webp){width: 300px}
