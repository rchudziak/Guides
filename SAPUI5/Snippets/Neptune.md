### Get elemeny by id
```Javascript
    let segBtn = {};

    if (sap.n) { //If run in launchpad
        segBtn = sap.ui.getCore().byId(sap.n.currentView.createId(segBtnId));
    } else { //If run standalone
        segBtn = sap.ui.getCore().byId(segBtnId);
    }
```

### Make function global across the launchpad
```Javascript
//Define the function
sap.ui.getCore().attachInit(function(data, navObj) {
     if (!sap.z) sap.z = {};
     if (!sap.z[localAppID]) {
         sap.z[localAppID] = {
             doUpload : function(event) {
                 console.log('doUpload: ' + localAppID);
             }
         };
     }
 });

//Then call it like this
sap.z.ZUI_NAD_MM_SHOPPING_CART.OCIimport();
```
### Expression binding
JSON Model
```
{AppState>/EDIT_MODE}
```
Table is bound - provide field name 
```
{= ${TYPE} === 'ZM01'}
```

Structure is bound - provide field name 
```
{= ${/TYPE} === 'ZM01'}
```
JSON Model based on two properties (OR)
```
{= ${AppState>/EDIT_MODE} || ${AppState>/PROCESS_MODE}  ? 'MultiSelect' : 'None' }

{= ${AppState>/EDIT_MODE} || ${AppState>/PROCESS_MODE}  }
```
