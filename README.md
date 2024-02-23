# CSS best practices you should know
Best practice tips to helping you become a CSS master

Cascading Style Sheets (CSS) are the backbone of web design and every front-end developer needs to go through them. Understanding how to wield their power effectively is crucial for creating beautiful, responsive, and maintainable web applications.

In this guide, we’ll explore some CSS best practices to consider when building applications!

Before we start, please keep in mind that it is imperative for developers — junior, senior or otherwise — to keep themselves updated on the best practices of whatever technology they’re focusing in. There is nothing preventing the best practices of today changing tomorrow.

### **1. Use a CSS Preprocessor**
CSS preprocessors like Sass or Less can help you write more organized and modular code. They offer features like variables, mixins, and nesting, which make your code more maintainable and reduce redundancy.

### **2. Organize Your Code**
Organization of code is significantly subjective, but there are general considerations that every developer should keep in mind.

   - **Use meaningful class and ID names:** Choose descriptive class and ID names that reflect the content or purpose of the element. For example, the class definitions in `<li className="navbar-link admin-link">` clearly refects that it’s a link in the navigation bar and that it’s a link that only admin users would see in the UI.
  
   - **Use consistent naming conventions:** Stick to a naming convention for your CSS class and ID definitions. Doing so will allow development teams to maintain consistency and improve legibility across their projects. BEM, OOCSS and SMACSS are popular and well documented naming conventions. Alternatively, you can always use a customized naming convention that fits your needs, so long as you adhere to it.
  
### **3. Optimize your selector definitions**
CSS selectors are used to locate the HTML elements you want to style. There are multiple ways to use selectors, which you can reference [here](https://www.w3schools.com/css/css_selectors.asp#:~:text=CSS%20selectors%20are%20used%20to,a%20specific%20relationship%20between%20them).

In general, you want to **avoid using overly specific** selectors that are too tightly coupled to the HTML structure. This can make your CSS hard to maintain. For example:

``` css
div#container > ul.navigation li.active a.btn-primary span.icon {
  /* CSS rules */
}
```

While this selector may work for the specific element you have in mind, it’s excessively specific. If any changes are made to the HTML structure, such as adding new elements or reordering them, this selector is likely to break. Instead, favor more flexible selectors, for example:

```css
.nav-link {
  /* CSS rules for navigation links */
}
```

In this example, we’re using a class-based selector that targets all navigation links. This is more maintainable and less prone to breaking if the HTML structure changes.

### **4. Understand CSS specificity rules**
[Specificity](https://www.w3schools.com/css/css_specificity.asp) is an internal calculation used by browsers to determine the CSS declaration that is the most relevant to an element and determines the property value to apply to that element.

Understanding how CSS specificity works allows us to optimize selectors and definitions in the most concise and clear way possible. Consider the following example:

``` css
.container p {
  color: blue;
}

.text {
  color: red;
}
```

In the first rule, `container p`, sets the text color to blue and in the second rule `.text`, sets the text color to red.

The rule `.container p` has a specificity of 0-1-1-0 (one class selector and one type selector). And the rule `.text` has a specificity of 0-0-1-0 (one class selector).

The rule with the higher specificity, which is `.container p`, takes precedence. Therefore, the text inside the `<p>` element will be blue.

### **5. Avoid using the !important property**
Touching upon the last two best practices above is the use of the `!important` property. You can use it to override ALL previous styling rules for that specific property. For example:

```css
.myParagraph {
  color: gray;
}

p {
  color: red !important;
}
```

In this case, the `p` tag will have a color of `red`.

As a general case, you should avoid using `!important` too much and rely instead on styling definitions through custom class namings and proper selector definitions.

The `!important` property is highly destructive in the sense that it overrides all previous styling for a specific property. As a project’s complexity and size grows, it becomes more difficult to maintain. A destructive definition such as this can be easy to miss and hard to locate when debugging, in addition to potentially introducing side-effects in styling definitions. Be wise about it’s use!

### **6. Minimize Nesting**
You shouldn’t nest your CSS selectors too deeply into a single parent, or parent to child relation. Take the following example:

```css
.wrapper {
  // wrapper styles here
  .container {
    // container styles here
    .card {
      // card styles here
      .content {
        // content styles here
        .paragraph {
          // paragraph styles here
          .paragraph-inner-text {
            // paragraph-inner-text styles here
          }
        }
      }
    }
  }
}
```

As your project grows and your stylesheet structure along with it, having huge swathes of nestes CSS code becomes difficult to maintain. Deeply nested styles can increase specificity, however, they also make your code harder to read.

Limit nesting to a reasonable level. Try to avoid nesting selectors more than 3 levels deep.

### **7. Modularize Your CSS**
Modularization involves breaking your CSS into small, reusable modules or components. This practice makes your codebase more maintainable and encourages code reusability, especially in larger projects. Each module should encapsulate the styles for a specific UI component or feature.

For example:

```css
/* Button Module */
.button {
  /* Button styles */
}

/* Navigation Module */
.navbar {
  /* Navbar styles */
}

/* Card Module */
.card {
  /* Card styles */
}
```

By organizing your CSS into modules, you can easily reuse the styles for buttons, navigation bars, and cards throughout your website without duplicating code. In addition, if you need to update the styling for a specific component, you can do so in one place, ensuring consistency.

In larger, more robust architectures, it will be even more efficient to divide your CSS into separate files and directories. A popular pattern to consider is the [7–1 pattern](https://sass-guidelin.es/#the-7-1-pattern), which relies on Sass.

### **8. Responsive Design**
Responsive design is the practice of creating web designs that adapt to different screen sizes and devices. Prioritizing responsive design ensures that an application looks and functions well on a variety of devices, from desktop computers to mobile phones.

### **9. Test Across Browsers**
Ensure that your styles work consistently across different browsers by testing and addressing compatibility issues. As a reference, you can use the platform [CanIUse](https://caniuse.com/#home) to verify if a CSS definition is compatible across all, or at least, a majority of browsers.

### **10. Documentation**
Documenting CSS code involves adding comments or creating external documentation that explains the purpose, usage, and important details of your CSS rules and styles.

Writing documentation is invaluable, especially when working on team projects, or simply when returning to your own code after some time. It is particularly useful in describing the inner functionalities of complex workarounds.

For more extensive documentation, consider creating a separate document or README file that explains the overall architecture of your CSS, such as naming conventions, and any specific guidelines or considerations for maintaining and extending the styles.

For example:

># CSS Documentation
>
>This document provides an overview of the CSS styles used in our project.
>
>## Structure
>
>Our CSS is organized into the following:
>
>1. **Components**: Styles related to reusable components, such as forms and buttons.
>2. **Layouts**: Styles for to main page layouts and elements related to layouts, such as containers, grids, headers and footers.
>
>## Naming Conventions
>
>We follow the BEM (Block Element Modifier) naming convention for our classes. For example:
>- `.block` for block-level components.
>- `.block__element` for elements within a block.
>- `.block--modifier` for modifiers that change a block's appearance.
>
>## Maintenance Guidelines
>
>- Avoid excessive nesting to keep our styles maintainable. At most consider 3 levels deep.

- If you’re interested in reviewing coding challenges, please feel free to check out the [Problem-solving](https://medium.com/@paulohfev/list/problemsolving-series-3727133f4336) series!

- And if also you’re interested in reading more articles, check out the [As a programmer](https://medium.com/@paulohfev/list/as-a-programmer-series-3d1e299837d1) series!