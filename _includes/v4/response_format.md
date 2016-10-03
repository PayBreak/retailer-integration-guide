## Response Format

All responses by default are formatted in json however you can change the response format to csv by adding the 
additional parameter `format=csv`

#### Example Request

```
GET {{ site.data.globals.api_prefix }}/aggregate-settlement-reports/:settlement-report?format=csv
```

#### Example Response

```
"Order Date","Notification Date",Customer,"Post Code","Application ID","Retailer Reference","Order Amount",Type,Deposit,"Loan Amount",Subsidy,Adjustment,"Settlement Amount"
03/09/2016,06/09/2016,"Mr Fillibert Labingi","TN12 6ZZ",2829,ALT-WA14-55e86a48a3a4,67800,Cancellation,-1000,-66800,-900,0,-68700
```
