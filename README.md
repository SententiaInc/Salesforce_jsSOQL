# Salesforce_jsSOQL
Simple Visualforce Example to Execute SOQL via Vanilla Javascript

Examples uses salesfoce connection.js to allow the user to enter test SOQL and see the results live from Salesforce


![alt text](https://github.com/SententiaInc/Salesforce_jsSOQL/blob/master/Salesforce_jsSOQL.PNG "Vanilla Javascript SOQL JSON Example")


user must include following script in Visualforce page: 

`<script src="../../soap/ajax/37.0/connection.js" type="text/javascript" />`

and add following HTML elements to the page body: 

`<button onclick="runSOQL()">Execute</button>`

`<input type="text" id="soql_input" size="128" value="Select Id From Contact"/><br/>`

Full code appended to this repository for easy testing

`<span id="output"/> `


    'var records = []; 
    sforce.connection.sessionId='{!$Api.Session_ID}';

    function runSOQL(){
         var soql = document.getElementById("soql_input").value;
         console.log(soql); 
         
         var result = sforce.connection.query(soql , {
         onSuccess : success, onFailure : failure});
         function success(result) {
         console.log(result);
         var it = new sforce.QueryResultIterator(result);
         var output = ""; 
         while(it.hasNext()){
              var record = it.next();
              output += JSON.stringify(record) + '<br/>'; 
        } 
        document.getElementById("output").innerHTML="Results: <br/>" + output;
    }
    function failure(error) {
        alert("An error has occurred " + error);
    }
    };'

