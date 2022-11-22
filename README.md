<!DOCTYPE html><html>
<head> <meta charset="UTF-8"> <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>menu items</title>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/handlebars.js/4.7.7/handlebars.min.js"></script>

      <!-- bootstrap, need to use https for these links -->
      <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.4.0/css/bootstrap.min.css">
	  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
      <script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.4.0/js/bootstrap.min.js"></script>

    <style> .btn{margin: 5px} </style>
</head>
<body>
  <div class="container">
      <h2>Select a Major</h2>
      <div style='padding: 5px;'> 
         <button type='button' class="btn btn-primary" onClick="getData('CIT Majors ')">CIT Majors</button> 
         <button type='button' class="btn btn-primary" onClick="getData(‘Business Majors’)”>Business Major</button>  
      </div>
  
  <h3>We filter our dataset by major</h3>

  <div id="menuTable"></div>

       <!-- Handlebars template -->
  <script type="text/x-handlebars-template" id="menuTemplate">
      <table class="table table-striped">
          <tr><th>Item</th><th>major</th><th>midterm</th><th>final</th></tr>
             {{#each rows}}
                <tr>
                     <td>{{name}}</td><td>{{major}}</td><td>{{midterm}}</td><td>{{final}}</td>
                </tr>
             {{/each}}
      </table>
  </script>

  <!-- application ajax code -->
  <script>
    async function getData(selected_major) {
        var response = await fetch('cit5students.json');   // this is an ajax GET request

        if(response.ok) {
            var data = await response.json();

            major_students = data.filter( (students) => students.major == selected_major );    // filter data array for selected meal items 
                
           var templateText = document.getElementById('menuTemplate').innerHTML;
           var compiledTemplateText = Handlebars.compile(templateText);   // get and compile template code
           compiledHtml = compiledTemplateText({ rows: major_students })      // apply data to template
           document.getElementById('menuTable').innerHTML = compiledHtml; 
       }
       else {
           document.querySelector('#menuTable').innerHTML = “Error occured or missing, try again”;
       }	
 
  }
</script>
</html>

