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
