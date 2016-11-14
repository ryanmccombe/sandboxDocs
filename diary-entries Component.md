# `<diary-entries>` Component

In order to display all the diary entries under a record, we need to create a presentational component

##### Starting Point / Assumptions
  - We have a `<diary-home>` root component
  - The `<diary-home>` component has all the relevant diaries on its view-model (vm)

##### Considerations
  - The component should handle UI logic only
  - The component should be stateless - it should not store or retrieve it's own data - data gets handed down to it by the `<diary-home>` component
  - When applying component CSS, be mindful that class names are global.  As these files get bundled together, you don't want your CSS files styling arbitrary elements around ProCon that happen to have the same class, or other CSS files styling yours.   Rather than declaring a class like `date-column`, use something like `diary-entries-date-column`

### 1. Scaffolding `<diary-entries>`
Create a diaryEntries directory under the diary feature directory.  Create the required files for this component:

  - `diaryEntries.js`
  - `diaryEntries.html`
  - `diaryEntries.css`

*Note: A specified controller is not needed for this component.  With no `controller` specified in the component definition, angular will provide a default blank controller, which keeps the code simple and is good enough for our current needs*

1. `diaryEntries.js` should register the `<diary-entries>` component with the same angular module `<diary-home>` is registered with

2. The component will need to accept the diary entries as one of its `bindings` - this should be a one-way binding using the `<` character ([ref](http://www.codelord.net/2016/05/19/understanding-angulars-one-way-binding/))

3. As we prefer controllers being called `vm`, we need to define that as the `controllerAs` property on the component definition.

4. The component should reference `diaryEntries.html` as its `templateUrl` using the `resolveUrl` service.  `diaryEntries.html` should just output the raw diary entries for now

5. For testing purposes, apply test styling to `<diary-entries>` in the `diaryEntries.css` file so we can be sure it is working.

6. Ensure the files are included in the postaward JS bundles in `BundleConfig.cs` (CSS file in the CSS bundle, and JS file in the JS bundle)

7. Include `<diary-entries>` in the template of the `<diary-home>` component, and pass the diary entries through to it using the bindings defined in `diaryEntries.js`

8. Ensure all the scaffolding is set up correctly by visiting the diary home page.  Make sure the component, its template, and its stylesheet are loading, and that the diary entries are being successfully passed through and displayed

##### Possible Solution
***`BundleConfig.cs`*** *(Work in Progress)*
```c#
//
```

***`diaryHome.html`*** *(Work in Progress)*
```html
<diary-entries data-diary-entries="vm.diaries" />
```
***`diaryEntries.js`*** *(Work in Progress)*
```javascript
//
```

***`diaryEntries.html`***
```html
{{vm.diaryEntries}}
```

***`diaryEntries.css`***
```css
diary-entries {
    color: red;
}
```

### 2. Presentation
With `<diary-entries>` successfully scaffolded and receiving data, it is that component's responsibility to handle the presentation of that data.

In ProCon development, the team would brainstorm and mock up ideas for how this could be done, and present those options and recommendations to the product stakeholders for feedback and decision.

For the purposes of development training, we can assume we have decided to display these records in the form of simple rows in a table.

1. Create an HTML table in diaryEntries.html
2. This table should have enough columns to allow the user to get an overview of each diary entry (it doesn't need all the information - later, a user will be able to click a row to view a single diary entry in full)
3. The table should have a row for every diary entry given to it - this can be achieved using angular's `ng-repeat` directive ([docs](https://docs.angularjs.org/api/ng/directive/ngRepeat))
4. Apply appropriate classes to the columns in the HTML, and set the widths of those classes in `diaryEntries.css`

##### Possible Solution
***`diaryEntries.html`*** *(Work in Progress)*
```html
<!--  -->
```

***`diaryEntries.css`*** *(Work in Progress)*
```css
/**/
```

### 3. UI Consistency
Our current policy for UI design offers 2 options:
1. The team uses a UI pattern that is already used somewhere else in the system, and references that existing feature / page
2. The team identfies that they want to create a new pattern, and engages Dan for help / approval

Option 1 is much more common and is what will be used here.  The specifics of the UI code is not broken down in the technical design but rather, the design includes a reference to the pattern we're using (a feature / page already in ProCon), and the developer is reponsible for getting their solution as close to that pattern as they can.

*Note: This doesn't just apply to styling - it includes things like phrasing and formatting (eg, dates)*

##### References for Design Patterns to Replicate:
- ***Tender Messaging Main Grid*** - Complicated grid that uses SlickGrid, but includes patterns like buttons around the grid, which will be needed for the diary home page
- ***Tender Messaging Story Grid*** - Much simpler grid that is closer in scope to what is being created here

##### Notes:
- ProCon has existing CSS for styling grids (TODO: `filename.css`) - this can be seen in the Story Grid reference.  This CSS can do most of the work - additional tweaks in `diaryEntries.css` may be warranted
 - ProCon has an angular formatter for standardising dates (TODO: `fileName.js`) - an example of its use can be found in both references (TODO: Confirm)

##### Possible Solution
***`diaryEntries.html`*** *(Work in Progress)*
```html
<!--  -->
```

***`diaryEntries.css`*** *(Work in Progress)*
```css
/**/
```