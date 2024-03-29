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
sap.z.ZUI_NAD_APP_NAME.doUpload();
 ```
 ### Pass temporary data to dialog
 ```Javascript
//Pass Data to dialog dialogObjectName.data("ParameterName", Value);
 dialogObjectName.data("ParameterName", Value);
 
 //Read Data assigned to dialog
 let value =  dialogObjectName.data("ParameterName");
 ```

### Expression binding
JSON Model
```Javascript
{AppState>/EDIT_MODE}
```
Table is bound - provide field name 
```Javascript
{= ${TYPE} === 'ZM01'}
```

Structure is bound - provide field name 
```Javascript
{= ${/TYPE} === 'ZM01'}
```
JSON Model based on two properties (OR)
```Javascript
{= ${AppState>/EDIT_MODE} || ${AppState>/PROCESS_MODE}  ? 'MultiSelect' : 'None' }

{= ${AppState>/EDIT_MODE} || ${AppState>/PROCESS_MODE}  }
```
### Dialog callback function
```Javascript
// Pass the function to the dialog
dlgAssignTechnician.callbackFunction = assignOperTechnician.bind(this);
dlgAssignTechnician.open();

//Then call it in the OK button
dlgAssignTechnician.callbackFunction();
```

### Use promises for two or more AJAX calls
```Javascript
   App.setBusy(true);
        Promise.all([getOnlineInitList(), getOnlineInitSearchHelps()]).then(function() {
            Notif.createNotification(oNotifDetails);
            App.setBusy(false);
        }).catch(function(reason) {
            App.setBusy(false);
            onAjaxError();
        });
```

### Find tree table model data suboordinates
```Javascript
let oTableData = modelTreeTable.getData();
let aSubordinates = this.findSubordinates(oTableData.children[0], object.OBJECT_ID);
 
    findSubordinates: function(obj, id) {
        let subordinates = [];
        if (obj.OBJECT_ID === id) {
            if (obj.children) {
                obj.children.forEach(child => {
                    subordinates.push(child);
                    subordinates = subordinates.concat(this.findSubordinates(child, child.OBJECT_ID));
                });
            }
        } else {
            if (obj.children) {
                obj.children.forEach(child => {
                    subordinates = subordinates.concat(this.findSubordinates(child, id));
                });
            }
        }
        return subordinates;
    },
```    
