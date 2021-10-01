I tried to put the following in the search bar:

`<script>alert()</script>`

And I saw an error in the console (F12). Tracing the error showed me that `</script>` wasn't expected there,  
which means it broke the script. So I changed my input to:

`</script><script>alert()</script>`

and solved the lab.