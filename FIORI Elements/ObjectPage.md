### Header Info
```
@UI: {
    headerInfo: {
        typeName: 'Travel',
        typeNamePlural: 'Travels',
        title: {
            type: #STANDARD, value: 'Description' --Title on object page header
        },
        description: {
            value: 'TravelID'  --Description on object page header
        }
    },
```

### Header Facet - Data Point
```
    @UI.facet: [
      {
          id: 'TravelHeaderPrice',
          purpose: #HEADER,
          type: #DATAPOINT_REFERENCE,
          position: 10,
          targetQualifier: 'PriceData'
      },
      {
          id: 'TravelHeaderOverallStatus',
          purpose: #HEADER,
          type: #DATAPOINT_REFERENCE,
          position: 20,
          targetQualifier: 'StatusData'
       }
  ]

@UI.lineItem: [{ position: 70}]
@UI.dataPoint: { qualifier: 'PriceData', title: 'Total Price'}
TotalPrice;  

@UI.lineItem: [{ position: 80, criticality: 'OverallStatusCriticality' }]
@UI.textArrangement: #TEXT_ONLY
@UI.dataPoint: { qualifier: 'StatusData', title: 'Status', criticality: 'OverallStatusCriticality' }
OverallStatus;
```

### Header Facet - Data Point - progress bar
In the main View annotation
```
 @UI.facet: [
    {
           id: 'BudgetSpend',
           targetQualifier: 'BudgetSpend',
           targetElement: '_SES_OrderValue', //Reference to the association
           type: #DATAPOINT_REFERENCE,   
           purpose: #HEADER,           
           position: 40                       
       }]
```
In the associated CDS View annotation
```
@UI.dataPoint: { visualization: #PROGRESS ,
               targetValueElement: 'OrderValue',
               qualifier: 'BudgetSpend',
               title: 'Budget Spend',
               criticality: 'SpendCriticality' }
ServiceEntries;
```

### Standard Facet - identification reference
```
  @UI.facet: [
    {
      label: 'General',
      id: 'Travel',
      type: #IDENTIFICATION_REFERENCE,
      purpose: #STANDARD,
      position: 10
    }
  ]
  
@UI.identification: [{ position: 10 }]
Description;    
```  

### Header Facet - identification reference
```
  @UI.facet: [
    {
         label: 'Administration',
         id: 'HeaderDetails',
         purpose: #HEADER,
         type: #IDENTIFICATION_REFERENCE,
         position: 10
    }
  ]
  
@UI.identification: [{ position: 10 }]
CreatedBy;    
```  


###  Fieldgroup Reference Facet 
```
  @UI.facet: [
    {
      id: 'Prices',
      purpose: #STANDARD,
      type: #FIELDGROUP_REFERENCE,
      label: 'Prices',
      position: 20,
      targetQualifier: 'PricesGroup'
    }
  ]
  
 @UI.fieldGroup: [ { qualifier: 'PricesGroup', position: 10} ]
 BookingFee;  
```

### Line Item Facet
```
    {
      id: 'Booking',
      purpose: #STANDARD,
      type: #LINEITEM_REFERENCE,
      label: 'Bookings',
      position: 20,
      targetElement: '_Booking'
    }

--Then line item annotations in _Booking entity
 @UI.lineItem: [ { position: 10 } ]
 BookingID;
 ```

### Collection Facet
```
  @UI.facet: [
-- Collection  
    {
      label: 'General Information',
      id: 'GeneralInfo',
      type: #COLLECTION,
      position: 10
    },
-- Standard Facet      
    {
      label: 'General',
      id: 'Travel',
      type: #IDENTIFICATION_REFERENCE,
      purpose: #STANDARD,
      parentId: 'GeneralInfo',
      position: 10
    },
-- Fieldgroup Reference Facet    
    {
      id: 'Prices',
      purpose: #STANDARD,
      type: #FIELDGROUP_REFERENCE,
      parentId: 'GeneralInfo',
      label: 'Prices',
      position: 20,
      targetQualifier: 'PricesGroup'
    }
  ]
  
```
