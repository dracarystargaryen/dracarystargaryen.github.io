import React, {useState, useEffect} from 'react';
import {ThemeProvider} from '@mui/styles';
import Button from '@mui/material/Button';
import './App.css';


const useLocalStorage = () => {
  let items = localStorage.getItem('items');

  if(items){
    return JSON.parse(localStorage.getItem('items'));
  } else {
    return [];
  }
}

const getItems = () => {
  let getItemsInput = localStorage.getItem('getItemsFromStorage')
  if(getItemsInput){
    return JSON.parse(localStorage.getItem('getItemsFromStorage'))
  } else {
    return [];
  }
}


function App() {
  const [add, addMeals] = useState({ items: "" });
  const [update, updateMeals] = useState(useLocalStorage());
  const [deletes, deleteMeals] = useState(getItems());


  useEffect(()=>{
    localStorage.setItem('items', JSON.stringify(add))
    localStorage.setItem('items', JSON.stringify(update))
    localStorage.setItem('items', JSON.stringify(deletes))
  },[add, update, deletes])

  const handleChange = (e) => {
    let name = e.target.name;
    let value = e.target.value;
    addMeals({ ...add, [name]: value });
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    if (!add.items) {
      alert("Please add an item");
    } else {
      const updateMeals = { ...add, id: new add().getItems().updateMeals().deleteMeals()};
      updateMeals([...update, updateMeals]);
      addMeals({ items: "" });
    }
  };

  const handleUpdateClick = (id) => {
    id.preventDefault();
    if (!update.items){
      alert("Please update");
    } else {
    updateMeals(update.filter(() => add.id !== id));
    const updates = update.filter((items) => items.id === id);
    deleteMeals.concat(updates);
    }
  };
  
  const handleDeleteClick = (id) => {
    deleteMeals(deletes.filter((items) => items.id !== id));
  };
  
    return(
      <div>
        <ThemeProvider>
  <meta charSet="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/materialize/1.0.0/css/materialize.min.css" />
  <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css" integrity="sha384-wvfXpqpZZVQGK6TAh5PVlGOfQNHSoD2xbE+QkPxCAFlNEevoEH3Sl0sibVcOQVnN" crossOrigin="anonymous" />
  <title>Calorie Counter</title>
  <nav>
    <div className="nav-wrapper blue">
      <div className="container">
        <a href="#" className="brand-logo center">Calorie Counter</a>
        <ul className="right">            
        </ul>
      </div>
    </div>
  </nav>
  <br />
  <div className="container">
    <div className="card">
      <div className="card-content">
        <span className="card-title">Add Meal / Food Item</span>
        <form className="col">
          <div className="row">
            <div className="input-field col s6">
              <input type="text" placeholder="Add Item" id="item-name" />
              <label htmlFor="item-name">Meal</label>
            </div>
            <div className="input-field col s6">
              <input type="number" placeholder="Add Calories" id="item-calories" />
              <label htmlFor="item-calories">Calories</label>
            </div>
            <Button onClick = {e => handleSubmit(e)} type = "submit" className = "add-btn btn blue darken-3">
              <i className="fa fa-plus" /> Add Meal
            </Button>
            <Button className="update-btn btn orange" onClick={handleUpdateClick}>
              <i className="fa fa-pencil-square-o" /> Update Meal
            </Button>
            <Button onClick= {() => handleDeleteClick()} className = "delete-btn btn red">
              <i className="fa fa-remove" /> Delete Meal
            </Button>
            <Button onClick= {handleChange} className = "back-btn btn grey pull-right">
              <i className="fa fa-chevron-circle-left" /> Back
            </Button>
          </div>
        </form>
      </div>
    </div>
    <h3 className="center-align">
      Total Calories: <span className="total-calories">0</span>
    </h3>
    <ul id="item-list" className="collection" />
  </div>
  </ThemeProvider>
</div>

    );
  }


export default App;
