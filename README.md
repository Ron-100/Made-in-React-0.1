1st
make this in root :
> npm init -y
> npm install concurrently --save-dev

2nd
add it root packege
"start": "concurrently \"npm run [for vite type 'dev' for core react type 'start'] --prefix [name - frontend folder]\" \"npm run start --prefix [name - backend folder]\""
{
  "scripts": {
    " add here "
    "test": "echo \"Error: no test specified\" && exit 1"
  }
}

3rd
change the the backend (for this application)
paste it -
const express = require('express');
const bodyParser = require('body-parser');
const cors = require('cors');

const { getStoredItems, storeItems } = require('./data/items');

const app = express();

app.use(cors());
app.use(bodyParser.json());

app.get('/items', async (req, res) => {
  const storedItems = await getStoredItems();
  res.json({ items: storedItems });
});

app.get('/items/:id', async (req, res) => {
  const storedItems = await getStoredItems();
  const item = storedItems.find((item) => item.id === req.params.id);
  res.json({ item });
});

app.post('/items', async (req, res) => {
  const existingItems = await getStoredItems();
  const itemData = req.body;
  const newItem = { ...itemData, id: Math.random().toString() };
  const updatedItems = [newItem, ...existingItems];
  await storeItems(updatedItems);
  res.status(201).json({ message: 'Stored new item.', item: newItem });
});

app.listen(8080, () => {
  console.log("✅ Backend running on http://localhost:8080");
});


4th
go backend folder and do this
> npm init -y
> npm install express body-parser cors

END
Go back to root 
> npm start