# JS_checkExceededDate
Get all date from a table and hide the exceeded date. Vanilla JavaScript

```HTML

 <h1>career</h1>

 <table class="table table-striped table-hover table-condensed table-societe">
 
  <tr>
  	<th>Publication date</th>
    <th>Job offer</th>
    <th>Location</th>
    <th>Contact</th>
    <th>Application deadline</th>
  </tr>

   <tr>
  	<td>07.11.2016</td>
  	<td><a href="#" target="_blank">Junior Developer</a></td>
  	<td>JonathanCharlet SA, Ch. des terrasses 10, 1400 Yverdon-les-Bains, Suisse</td>
  	<td><a href="mailto:jonathan.charlet@bluewin.ch">jonathan.charlet@bluewin.ch</a> ou par poste à Ressources Humaines</td>
    <td>&nbsp;</td>
  </tr>

   <tr>
  	<td>21.09.2016</td>
  	<td><a href="#" target="_blank">DBA</a></td>
  	<td>JonathanCharlet SA, Ch. des terrasses 10, 1400 Yverdon-les-Bains, Suisse</td>
  	<td><a href="mailto:jonathan.charlet@bluewin.ch">jonathan.charlet@bluewin.ch</a> ou par poste à Ressources Humaines</td>
  	<td>31.12.2016</td>
  </tr>
  
  <tr>
   <td>21.09.2016</td>
   <td><a href="#" target="_blank">Médiamaticien</a></td>
   <td>JonathanCharlet SA, Ch. des terrasses 10, 1400 Yverdon-les-Bains, Suisse</td>
   <td><a href="mailto:jonathan.charlet@bluewin.ch">jonathan.charlet@bluewin.ch</a> ou par poste à Ressources Humaines</td>
   <td>1.12.2016</td>
 </tr>


  <tr>
  	<td>14.07.2016</td>
    	<td><a href="#" target="_blank">Informaticien de gestion</a></td>
  	<td>JonathanCharlet SA, Ch. des terrasses 10, 1400 Yverdon-les-Bains, Suisse</td>
  	<td><a href="mailto:jonathan.charlet@bluewin.ch">jonathan.charlet@bluewin.ch</a> ou par poste à Ressources Humaines</td>
    	<td>2.1.2017</td>
  </tr>

    <tr>
    	<td>14.07.2016</td>
     	<td><a href="#" target="_blank">Informaticien de gestion</a></td>
    	<td>JonathanCharlet SA, Ch. des terrasses 10, 1400 Yverdon-les-Bains, Suisse</td>
    	<td><a href="mailto:jonathan.charlet@bluewin.ch">jonathan.charlet@bluewin.ch</a> ou par poste à Ressources Humaines</td>
      	<td>02 1 17</td>
    </tr>

      <tr>
      	<td>14.07.2016</td>
        <td><a href="#" target="_blank">Informaticien de gestion</a></td>
      	<td>JonathanCharlet SA, Ch. des terrasses 10, 1400 Yverdon-les-Bains, Suisse</td>
      	<td><a href="mailto:jonathan.charlet@bluewin.ch">jonathan.charlet@bluewin.ch</a> ou par poste à Ressources Humaines</td>
        <td>02.1.2117</td>
      </tr>
      
```



```JavaScript
	function exceededDate(i){

		// +1 because of the first TR tag who has no TD tags but TH tags instead
		document.getElementsByTagName('tr')[i+1].style.display="none";
	}

	function checkDate(){

		// get current date informations
		var d = new Date();
		var currentJ = d.getDate();
		var currentM = d.getMonth()+1;
		var currentA = d.getFullYear();

		var innerDate;
		var innerj;
		var innerm;
		var innera;
		var posPoints = [];

		//number of TR tags in the document - the first one who is the title
		var nbtr=document.getElementsByTagName('tr').length -1;

		// For each TR tags
		for(i=0;i<nbtr;i++){

			//TD tag number 4 (start at 0) in each TR tag + for each TR tag the date is at the 5th instanciation of TD tag
      targetTD=4+(5*i);
			innerDate = document.getElementsByTagName('td')[targetTD].innerHTML;

			//Erase a possible human mistake like a space character at the begining
			if (innerDate.substring(0,1) == ' '){
				innerDate =  innerDate.substring(1,innerDate.length);
			}

			if (innerDate.length>2){

				//Get the position of the separators (. or - or /)
				for (j=0; j<=innerDate.length; j++){
					var x=0+1*j;
					var y=1+1*j;
					if ( (innerDate.substring(x,y)=='.') || (innerDate.substring(x,y)=='-') || (innerDate.substring(x,y)=='/') || (innerDate.substring(x,y)==' ') ){
						posPoints.push(j);
						}
				}
          // The day is from the begining to the first point
					innerj = innerDate.substring(0,posPoints[0]);

          // The month is from the first point to the second point
					innerm = innerDate.substring(posPoints[0]+1,posPoints[1]);

          // The year is from the second point to the end
          				innera = innerDate.substring(posPoints[1]+1,innerDate.length);
					posPoints = [];

          // if the year is written with only the 2 last digit (innera is casted like a string and not like a number so we do a simple concatenation of a number and a string)
          if (innera.length==2){
            innera = 20 + innera;
          }

        // is the year exceeded?
				if (currentA>innera) {
						exceededDate(i);
				}

        // is the year the current year?
				else if (currentA==innera){

          // is the month exceeded?
        	if (currentM>innerm) {
						exceededDate(i);
					}

          // is the month the current month?
					else if (currentM==innerm){


            // is the day exceeded?
						if (currentJ>innerj) {
							exceededDate(i);
						}
					}
				}
			}
		}
	}
	checkDate();

```

***

_Jonathan Charlet_
