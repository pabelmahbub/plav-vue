# plav-vue

### vue create my-app
### how to create a mock server:
```
create a folder named db in root and create a file named db.json and paster some json data:
```
install: npm i json-server      
npx json-server --watch data/db.json 
```
```
Now connect it:
    fetch('http://localhost:3000/projects')
    .then(response => response.json())
    .then(data => this.projects = data)
    .catch(err => console.log(err.message))
  },
```  
### Install and use Bootstrap5:
```
npm i bootstrap
```
```
in main.js:
import 'bootstrap/dist/css/bootstrap.css';
import 'bootstrap/dist/js/bootstrap.bundle.js'
```
