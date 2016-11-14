# Viewing a Single Diary Entry

In order to display and maintain an individual diary entry, we require a component to manage this

##### Starting Point / Assumptions
  - We have a `<diary-entries>` component which includes a list of diary entries
  - We have a RESTful endpoint - eg `/diaries/id` - to retrieve an individual diary entry

##### Considerations
  - `<eoe-form>` attempts to combine both view and edit functionality in a single component composition
  - As we're not creating a single page application, data needs to be passed from the diary home page to the new page we're creating
    - We typically use url querystrings for this purpose, eg, `/diary-entry?id=123`

### 1. Scaffolding `<diary-entry>`
Create a new page: Diary_Entry.aspx in the diary feature directory.  This page should use the same boilerplate as Diary_Create.aspx - replacing the `<diary-create>` component with `<diary-entry>`

To house this new component, create a diaryEntry directory under the diary feature directory.  Create the required files for this component:

  - `diaryEntry.js`
  - `diaryEntry.controller.js`
  - `diaryEntry.html`
  - `diaryEntry.css`

1. `diaryEntry.js` should register the `<diary-entry>` component with the same angular module `<diary-home>` is registered with
2. Scaffold an empty Angular controller in diaryEntry.controller.js and create a test vm property
3. Set that controller as the component's controller in the component definition file
4. As we prefer controllers being called `vm`, we need to define that as the `controllerAs` property on the component definition
4. The component should reference `diaryEntry.html` as its `templateUrl` using the `resolveUrl` service.  `diaryEntry.html` should just output the test viewmodel property for now
5. For testing purposes, apply test styling to `<diary-entry>` in the `diaryEntry.css` file so we can be sure it is working.
6. Ensure the files are included in the postaward JS bundles in `BundleConfig.cs` (CSS file in the CSS bundle, and JS files in the JS bundle)
7. Ensure all the scaffolding is set up correctly by visiting the diary entry page URL.  Make sure the component, its template, and its stylesheet are loading, and that the test VM property is correctly displayed

##### Possible Solution
***`BundleConfig.cs`*** *(Work in Progress)*
```c#
//
```

***`Diary_Entry.aspx`*** *(Work in Progress)*
```html
<!-- -->
```
***`diaryEntry.js`*** *(Work in Progress)*
```javascript
//
```

***`diaryEntry.controller.js`*** *(Work in Progress)*
```javascript
//
```

***`diaryEntry.html`*** *(Work in Progress)*
```html
{{vm.test}}
```

***`diaryEntry.css`*** *(Work in Progress)*
```css
diary-entry {
    color: red;
}
```

### 2. Handling the Diary ID
When a user clicks a row on the `<diary-entries>` grid, they need to be sent to this new page.  The component needs to know which diary entry to display.  This will need passed from the `<diary-entries>` component to the `<dairy-entry>` component using the URL querystring.

1. Introduce a custom controller to the `<diary-entries>` component.  This will require creating a `diaryEntries.controller.js` file in the correct directory, and adding a `controller` property to the component definition
2. Update `diaryEntries.html` - when a user clicks on a row, a function needs called on this new controller, and the ID of the diary clicked on will need to be an argument.  Use angular's `ng-click` directive ([docs](https://docs.angularjs.org/api/ng/directive/ngClick))
3. Implement this function in the controller - it needs to redirect the user to the new DiaryEntry page and take the ID from the arguments and put it in the querystring (eg, `Diary_Entry.aspx?diary-id=123`)
4. The `<diary-entry>` component needs to retrieve this ID.  This can be done in many ways: the ASPX page can get the ID and pass it into the component as a binding (reference: `MessagesList.aspx`), the component controller can get it itself using the global ProConAngular object (reference: `controller-DataGrid-view.js`) or the controller can get it without global dependencies (reference: tenderMessagingContainer.controller.js)
5. Either solution should result in the ID being available - update your template to display this ID to test

##### Possible Solution
***`diaryEntries.html`*** *(Work in Progress)*
```html
<!-- -->
```

***`diaryEntry.controller.js`*** *(Work in Progress)*
```javascript
//
```

***`Diary_Entry.aspx.cs`*** *(Work in Progress)*
```c#
//
```

***`Diary_Entry.aspx`*** *(Work in Progress)*
```html
<!-- -->
```

***`diaryEntry.js`*** *(Work in Progress)*
```javascript
//
```

***`diaryEntry.controller.js`*** *(Work in Progress)*
```javascript
//
```

***`diaryEntry.html`*** *(Work in Progress)*
```html
{{vm.test}}
```

### 3. Retrieving the Diary Entry Data
With the ID available, we're now ready to make a request to the API and get the data for our entry.

1. Update `service-DiaryApi.js` with a new method for getting a single diary entry, given a diary ID.  This method should defer to serviceProConRestApi.call
2. Update ``diaryEntry.controller.js` with a function that will trigger the API request through `service-DiaryApi.js` and update the VM when the request completes
3. Update `diaryEntry.controller.js` with an `$onInit` lifecycle hook ([ref](http://blog.thoughtram.io/angularjs/2016/03/29/exploring-angular-1.5-lifecycle-hooks.html))
to call this function when the component is initialised
4. Update the component template to display this data, and ensure everything is working

##### Possible Solution
***`service-DiaryApi.js`*** *(Work in Progress)*
```javascript
<!-- -->
```

***`diaryEntry.controller.js`*** *(Work in Progress)*
```javascript
//
```

### 4. Presentation
Situations where we have to display a record to a user but also edit it (coming later) are common in ProCon, and we have created the `<eoe-form>` architecture to support this.

1. Duplicate over the `<eoe-form>` component from diaryCreate.html into diaryEntry.html
2. Create a vm property on the controller to control whether or not the form is in edit mode - this should be false initially
3. Pass that property into the `in-edit-mode` binding of eoe-form
4. In order to display your data, the `data-value` of each element must reference where this data is stored on your viewmodel - eg, if you're storing your entry on `vm.diary` and the comment is stored as `comment`, the `value` would be `vm.diary.comment`
5. Files will need displayed in a similar fashion to other areas in ProCon - eg, Tender Message Attachments


### 5. UI-Consistency
`<eoe-form>` and its child components have standardised styling embedded - they should be inherently consistent 