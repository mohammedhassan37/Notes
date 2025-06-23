# Notes

### Props :

**Step 1:**  
Create `const products = []`, this is an array.

Then do `[{}]` inside of the array to add your products. Example:

```js
const products = [
  {
    img: xImage,
    title: '1',
    price: '$20.00',
    reviews: '★★★★☆',
    stock: 'In Stock'
  },
  {
    img: xImage,
    title: '2',
    price: '$20.00',
    reviews: '★★★★☆',
    stock: 'In Stock'
  }
];

export default products;
```

That creates two props that can be used.

---

**Step 2:**  
Create a `ProductCard` component that receives those props:

```js
function ProductCard(props) {
  return (
    <div className="product-card">
      <img src={props.img} alt={props.title} />
      <h4>{props.title}</h4>
      <p className="price">{props.price}</p>
      <p className="reviews">{props.reviews}</p>
      <p className={props.stock === 'In Stock' ? 'in-stock' : 'out-stock'}>
        {props.stock}
      </p>
    </div>
  );
}

export default ProductCard;
```

To use the props, write `{props.x}` depending on what prop you want to access.

After creating the props and the template, you need to **map** through them.

---

### Mapping

**What is mapping?**  
Mapping is something that goes through an array and creates a new item — in our example, a new `ProductCard`.

```js
import products from '../Product';
import ProductCard from '../components/ProductCard';
import '../styles/Shop.css';

function Shop() {
  return (
    <div className="shop-page">
      <div className="product-grid">
        {products.map((product, index) => (
          <ProductCard key={index} {...product} />
        ))}
      </div>
    </div>
  );
}

export default Shop;
```

---

**Step: Importing**  
You need to import everything you’ll use: the products array and the `ProductCard` component.

**Step: Mapping**  
After the imports, you map through the `products` array to create a card for each one.

---

### Grid Display:

```css
display: grid;
gap: 1.5rem;
grid-template-columns: repeat(5, 1fr);
grid-template-rows: repeat(3, auto);
```

This creates a grid of **5 columns and 3 rows**, with a `1.5rem` gap between each item.

---

![image](https://github.com/user-attachments/assets/4b325bdb-071b-4d10-8a36-b10c52d9b185)

---

### FA icons

**step 1: Import**

```import { FaShoppingBasket } from 'react-icons/fa';```

{} is subject to change depending on the icons you want

**step 2: implementing**

```<Link className="nav-items basket" to="/basket"><FaShoppingBasket/></Link> ```
<FaShoppingBasket/> 

to intialise it.

---

### Form Submission/validation

**Step 1: import and intialise**

```
import { useState } from 'react';

function Contact() {
  const [formData, setFormData] = useState({
    firstName: '',
    lastName: '',
    email: '',
    phone: '',
    category: '',
    message: ''
  });
```
Above imports useState from react.

FormData holds all of my values, e.g firstName, and they are all set to blank

SetFormData is a function to update my formData, as in it updates the firstName and etc.

---
**Step 2: Validation Errors**

```
  const [errors, setErrors] = useState({});
```
Errors: Will hold the errors from the different fields, and uses useState. and useState is empty. i.e there are no errors currently.
setErrors: will update this state

----

**Step 3: Input changes**

```
  const handleChange = e => {
    const { name, value } = e.target;
    setFormData(prev => ({ ...prev, [name]: value }));
  };
```
---

**Step 4: Input changes**

```
  const handleChange = e => {
    const { name, value } = e.target;
    setFormData(prev => ({ ...prev, [name]: value }));
  };
```
Defines a function with parameter e (the event).

Extracts name and value from the input that triggered the event.

Updates the formData state by copying the previous values and setting the changed field (name) to the new value.

---

**Step 5: Validation**

```
  const validate = () => {
    let tempErrors = {};
    if (!formData.firstName.trim()) tempErrors.firstName = 'First Name is required';
    if (!formData.lastName.trim()) tempErrors.lastName = 'Last Name is required';
    if (!formData.email.trim()) tempErrors.email = 'Email is required';
    else if (!/\S+@\S+\.\S+/.test(formData.email)) tempErrors.email = 'Email is invalid';
    if (!formData.category.trim()) tempErrors.category = 'Please select a topic';
    if (!formData.message.trim()) tempErrors.message = 'Message is required';
    return tempErrors;
  };
```
Checks what has an error/not filled in.
tempErrors (object) are the errors that you get in the current cycle of form submission
Lastly it returns tempErrors, until there is nothing empty


---

**Step 6: Submit Handler**

```
  const handleSubmit = e => {
    e.preventDefault();
    const validationErrors = validate();
    setErrors(validationErrors);

    if (Object.keys(validationErrors).length === 0) {
      alert('Your email has been sent.');
      // Here you could reset form or actually send data
      setFormData({
        firstName: '',
        lastName: '',
        email: '',
        phone: '',
        category: '',
        message: ''
      });
      setErrors({});
    }
  };
```
creates a function called handleSubmit with a parameter of e.
the parameter e, with the help of preventDefault. e.preventDefault doesnt allow the page to refresh when submitted
const validationErrors = validate uses the validate function
setErrors(validationErrors) will update the errors inside of validate

then it finally checks if there are any validation errors happening in the validate function. if not it will equal to 0 and then alert user the email has been sent, and sets the formdata back to empty,
and setErrors to blank once again
