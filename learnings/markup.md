## 1. Structure a site using semantic HTML to aid accessibility
### Examples of new semantic tags
```
<figure>
  <figcaption> 
  ...
  </figcaption>
</figure>
```
These included margins and other styles applied to both

```
<group>
  ...
</group>
```
To replace divs, includes styling

- all used in aid of accessibility.


## 2. Ensure a web page is readable for screen readers
Because of our emphasis on semantics there was very little need for aria labels to help screen readers. Exceptions being in the dropdown list in the nav >

```
<button type="button"
    id="btnSubmenu"
    aria-expanded="true"
    aria-controls="id_submenu"> Contact ˅</a>
<ul>
    id="id_submenu">
    <li>
       ...
    </li>
    <li>
      ...
    </li>
</ul>
```

and also in the basket. This scenaria was probably avoidable.

```
<hr aria-hidden="true"> 
```


## 3. Ensure our UI has sufficient colour contrast so that everyone can perceive it comfortably

![Screenshot 2023-02-06 at 19 44 26](https://user-images.githubusercontent.com/44851616/217069510-4f1a4ec1-f954-4b57-88c2-15d4e512f8d8.png)

Thereby by lighthouse standards i have sufficient colour contrast


## 4. Use various tools to check that our website meets accessibility criteria

As shown above lighthouse results were 100%.

Also used screen reader before reviews or after big changes to ensure only relevant information is read making it quicker to run through a page for screen reader users.


## 5. Use CSS media queries to ensure our content is always presented effectively on screens of different sizes


Since we implemented a mobile first approach we have used min-width rather than max-width.

```
@media (min-width:700px) {
  .grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(18rem, 1fr));
      gap: 1rem; 
    }
}
```

```
@media screen and (prefers-color-scheme: dark) {           
  :root {
      --background-color: #000411;
      --primary-color: #0d0718;
      --tab--color: #533f2c;
      --secondary-color: #060d1a;
      ...
    }
}
```

## 6. Demonstrate a mobile-first approach to building a website

This is evidence of mobile first since we came back to media queries after we were happy with the styling done on a mobile format. This snippet suggests we wanted to make changes once the viewport-width was beyond 700px (desktop).

```
@media (min-width:700px) { ... }
```

## 7. Use CSS variables to apply repeated colours to HTML elements

```
:root {
    --background-color: #b0f4aa;
    --primary-color: #e4bb7d;
    --tab--color: #eeda98;
    --secondary-color: #ecffe6;
    --accent-color-1: #ffeaa5;
    --accent-color-2: #e3e3e3;
    --nav--a--color: #18272F;
    --font-colour: #1a1b1c;
    --form-colour: rgb(173, 166, 166);
}

```

## 8. Use CSS Flexbox to style children in a single-direction layout (ie a row or a column)

```
.row {
    display: flex;
    gap: 0.5rem;
}
    .row__nogap {
        gap: 0rem;
    }

.row__wrap {
    flex-wrap: wrap;
}

```


## 9. Use CSS Grid to style children in two-direction layout

```
form__grid_on-desktop {
            display: grid;
            justify-items: end;
            align-items: center;
            grid-template-columns: 15rem 15rem;
            grid-template-rows: min-content min-content;
            grid-template-areas: 
                "main sidebar";
        }

```


## 10. Ensure our Git commit history tells a coherent story

Definitely still learning but when ignoring merge commits there is a clear path of bug fixes and development through the commit history.

![Screenshot 2023-02-06 at 20 39 01](https://user-images.githubusercontent.com/44851616/217080096-6b3f1a71-a854-462d-9398-3d439db91334.png)


## 11. Use the appropriate input types in HTML forms for gathering different types of information

```
<input
  class="margin-0 qoute-input"
  type="radio"
  name="rat"
  value="ratR"
  id="ratR"
 >
```
```
<input class="form--fields qoute-input"
  type="number"
  name="quantity" value="0"
  id="quantity1" min="0" max="200" size="3ex"
>
```

These two snippets suggest that this form below does use the correct inptu types; radio and number respectively. Radio that only allows one within a group to be checked. Number giving a numeric input with the up down, increment and decrement feature.


![Screenshot 2023-02-06 at 20 36 02](https://user-images.githubusercontent.com/44851616/217079470-33fb1963-64e1-4fe0-8797-8a8f727a861d.png)
