********************************* This is the 6 step for server side setup **************************************** 

1.initialize first:  <code>**npm init**  </code>

2.install pacakge:  <code>**npm i body-parser cors dotenv express mongodb nodemon**  </code> 

3.package.json file: check all package intall or not &&  
inside scripts add this two line:  <code>"start": "nodemon index.js", "start-dev": "node index.js", </code>

4.create .env file and inside it. type: USER=mongodbUser PASSWORD=mongodbPassword from mongodb  

5.inside index.js code already ready for you(nisharga_kabir_mondo_DB_only_other_people_may_change_mongodb_clients_inside_index.js}). 

6.inside index.js after (await client.connect(); dbCollection name).. your code inside here 



********************************* This is the 6 step for server side ****************************************
 
################### Github create repositories and all code push at once(just change origin) ###############################


<code>  echo "# nisharga" >> README.md && git init && git add README.md && git commit -m "first commit" && git branch -M main && git remote add origin https://github.com/nisharga/tedt.git && git push -u origin main  </code>


<code> git add . && git commit -m "second commit" && git push  </code>

################### Github create repositories and all code push at once(just change origin) ###############################

########################### Create a server side app && host in heroku ################### 
if already login heroku && and already all code push in github && (.env file, .gitignore file, 
port use is .env, process.env.PORT use in index.js) then just type ###############################



<code>heroku create</code>

<code>git push heroku main</code>

# Firebase Login And Create a project after that open Hosting(If u wants firebase deploy)

<code>firebase login</code>
	
<code>firebase init</code>

(If login not work. altanative this 2 code.)
	
<code>firebase login --interactive</code>
	
<code>firebase init hosting)</code>

<h4>Follow This Process</h4>

<code>Are u proceed: Y</code>
	
<code>Then select: Github action deploy</code>
	
<code>Then select: Use an existing project</code>
	
<code>Then select: the project name you create on web</code>

<code>Then type which directory you want to deploy public directory: build</code>

<code>configure single-page-app: Y</code>

<code>Deploys with gitHub: N</code>

this type this 2 everyTime changeing.......

<code>npm run build</code>
	
<code>firebase deply</code>



****************************** CRUD OPERATION Using MongoDB ************************************* 

################################## CREATE ###################################
	
// insertOne product to database(Server side)
	
	 
	
    app.post("/addproduct", async (req, res) => {
      const data = req.body;
      const result = await productCollection.insertOne(data);
      console.log(result, "product create on db");
    });
		
		 
			
// insertOne product to database end.

 // insertOne product for (Client side)
 
 
    fetch("https://localhost:5000/addproduct", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify({
        product: "alu", 
      }),
    })
      .then((response) => response.json())
      .then((data) => {
        console.log("Success:", data);
      })
      .catch((error) => {
        console.error("Error:", error);
      });
      
      
 // insertOne product for Client side
 
################################## CREATE ##################### 
 
################################## READ ####################### 

    // get a product from databse using id (Server side) 
    
    
    app.get("/product/:id", async (req, res) => {
      const id = req.params.id;
      const query = { _id: ObjectId(id) }; 
      const cursor = productCollection.find(query);
      const data = await cursor.toArray();
      res.send(data);
    });
    
    
    //  get a product from database end... ifSearchByEmail: just type: query = {email: id}
 

	//(Client side) get a product from databse using id 

	 
	
	const [singleProduct, setsingleProduct] = useState();
 	 useEffect(() => {
   		 const url = `https://localhost:5000/product/${id}`;
    		 fetch(url)
     		 .then((res) => res.json())
      		.then((data) => setsingleProduct(data));
  	}, [setsingleProduct]);
  	
	 
  
	// get a product from databse using id (Client side)

################################## READ ####################################

################################## UPDATE ####################################

    // update or upsert a data from database (Server side) 
    
    
    app.put("/deliverystatus/:id", async (req, res) => {
      const id = req.params.id;
      const query = { _id: ObjectId(id) };
      const data = req.body;
      const update = { $set: data };
      const options = { upsert: true };
      const result = await orderCollection.updateOne(query, update, options);
      console.log(data, "deliverystatus updated");
    });
    
    
    //  update or upsert a data from database end
	
    // update a data from databse (Client side)
    
	fetch(`https://localhost:5000/deliverystatus/${id}`, {
      method: "PUT",
      headers: {
        "Content-type": "application/json",
      },
      body: JSON.stringify({
        shipping: "Delivered",
      }),
    })
      .then((response) => response.json())
      .then((json) => {});
      
      
     // update a data from databse end
      
     
################################## UPDATE ####################################


################################## DELET ####################################

   // delet a product from database (Server Side)
   
   
    app.delete("/myitems/:id", async (req, res) => {
      const id = req.params.id;
      const query = { _id: ObjectId(id) };
      const result = await orderCollection.deleteOne(query);
      if (result.deletedCount === 1) {
        console.log("Sucessfully deleted ");
      }
      res.send(result);
    });

    // delet a product from database end 

    // delet a product from database(Client Side)
       
       
	fetch(`https://glacial-sierra-36711.herokuapp.com/myitems/${id}`, {
              method: "DELETE",
            })
        .then((res) => res.json())
        .then((val) => {
                if (val.deletedCount > 0) {
                  console.log(val, "val deleted");
                  window.location.reload();
                }
              });
	      
	      
    // delet a product from database end 
################################## DELET ####################################



# Axios CURD operation

<h3>(THIS IS FOR CLIENT SITE)</h3>

<code>npm install axios</code>

<code>const axios = require("axios").default;</code> (For App.js)

# GET

     axios
      .get("http://localhost:5000/user")
      .then(function (response) {
        setUser(response.data);
      })
      .catch(function (error) {
        console.log(error);
      })
      .then(function () {
        // always executed
      });

# POST using async

    (async () => {
      await axios
        .post("http://localhost:5000/adduser", {
          name: name,
          email: email,
        })
        .then(function (response) {
          console.log(response);
        })
        .catch(function (error) {
          console.log(error);
        });
     })();
     
# UPDATE

     axios
      .put(`http://localhost:5000/user/${id}`, {
        name: "NISHARGA",
      })
      .then(function (response) {
        console.log(response);
      })
      .catch(function (error) {
        console.log(error);
      });
      
     
# DELETE

      axios
      .delete(`http://localhost:5000/userdelet/${id}`)
      .then(function (response) {
        console.log(response);
      })
      .catch(function (error) {
        console.log(error);
      });
      
      

