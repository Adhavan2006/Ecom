# TISSO VISON E-commerce Component System

This project has been restructured into a component-based architecture for better maintainability, customization, and functionality.

## Project Structure

```
E-commerce/
├── index.html                          # Main HTML file
├── css/
│   └── style.css                      # Main stylesheet with component styles
├── js/
│   ├── app.js                         # Main application orchestrator
│   ├── components/
│   │   ├── BannerComponent.js         # Banner section component
│   │   ├── ProductGridComponent.js    # Product grid component
│   │   └── ProductModalComponent.js   # Product popup modal component
│   ├── utils/
│   │   ├── CartManager.js             # Shopping cart functionality
│   │   └── Customizer.js              # Content customization system
│   ├── script.js                      # Legacy compatibility bridge
│   └── script.js.backup              # Original script backup
└── public/                            # Product images
```

## Components Overview

### 1. Banner Component (`BannerComponent.js`)
- **Purpose**: Manages the top banner and hero sections
- **Features**:
  - Customizable text content (banner text, hero title, descriptions)
  - Animated buttons with hover effects
  - Mobile sidebar navigation
  - Smooth scrolling to product section
- **Customizable Elements**:
  - Brand name
  - Top banner text
  - Button text
  - Hero title and description
  - Shop button text
  - Sustainable message

### 2. Product Grid Component (`ProductGridComponent.js`)
- **Purpose**: Displays the product grid with selectable products
- **Features**:
  - Dynamic product rendering
  - Customizable product selection (6 products from available pool)
  - Responsive grid layout
  - Product click/touch handling
  - Section title customization
- **Product Management**:
  - Add/remove products
  - Update product information
  - Filter products for display

### 3. Product Modal Component (`ProductModalComponent.js`)
- **Purpose**: Handles the product detail popup
- **Features**:
  - Dynamic variant rendering (colors, sizes)
  - Stock management and availability checking
  - Add to cart functionality
  - Size dropdown with stock validation
  - Color selection with visual feedback
  - Mobile-optimized interactions

### 4. Cart Manager (`CartManager.js`)
- **Purpose**: Manages shopping cart operations
- **Features**:
  - Add/remove/update cart items
  - Local storage persistence
  - Stock validation
  - Cart calculations (subtotal, tax, shipping)
  - Notification system
  - Export cart data

### 5. Customizer (`Customizer.js`)
- **Purpose**: Content management and customization system
- **Features**:
  - Live content editing
  - Product selection management
  - Configuration import/export
  - Local storage for settings
  - Real-time preview updates

## Usage Instructions

### Opening the Customizer
1. **Keyboard Shortcut**: Press `Ctrl + E`
2. **Click Button**: Click the gear icon (⚙️) in the top-left corner

### Customizing Content
1. Open the customizer panel
2. Edit text fields for banner content
3. Select/deselect products for the grid
4. Click "Save Changes" to apply
5. Use "Export Config" to save settings

### Adding Products to Cart
1. Click on any product in the grid
2. Select color and size in the modal
3. Click "ADD TO CART" button
4. Item will be added with notification

### Keyboard Shortcuts
- `Ctrl + E`: Toggle customizer
- `Ctrl + Shift + C`: Clear cart (with confirmation)
- `Ctrl + Shift + S`: Show cart summary
- `Escape`: Close modal or customizer

## Developer Functions

Access these in the browser console:

```javascript
// Show current app state
TissoVisonDev.showState();

// Open customizer programmatically
TissoVisonDev.openCustomizer();

// Show cart contents
TissoVisonDev.showCart();

// Access legacy functions
TissoVisonLegacy.getProducts();
TissoVisonLegacy.getCart();
TissoVisonLegacy.getConfig();

// Access main app instance
TissoVisonApp.getComponent('productGrid');
TissoVisonApp.getUtil('cartManager');
```

## Customization Examples

### Adding a New Product
```javascript
const newProduct = {
    id: 7,
    name: "New Product",
    price: "299,00€",
    image: "public/new-product.png",
    colors: ["Red", "Blue"],
    sizes: ["S", "M", "L"],
    description: "Product description",
    variants: [
        { id: 'red-s', color: 'Red', size: 'S', stock: 10, sku: 'NP-RED-S' }
        // ... more variants
    ]
};

TissoVisonApp.getComponent('productGrid').addProduct(newProduct);
```

### Updating Banner Text
```javascript
TissoVisonApp.getComponent('banner').updateConfig({
    heroTitle: "New Hero Title",
    heroDescription: "New description text"
});
```

### Accessing Cart Data
```javascript
const cartManager = TissoVisonApp.getUtil('cartManager');
const cartData = cartManager.exportCart();
console.log('Total items:', cartData.count);
console.log('Total price:', cartData.total);
```

## Event System

The application uses a custom event system for component communication:

### Available Events
- `productSelected`: Fired when a product is clicked
- `addToCart`: Fired when adding item to cart
- `cartUpdated`: Fired when cart changes
- `customizerUpdate`: Fired when customizer settings change
- `appReady`: Fired when app initialization is complete

### Listening to Events
```javascript
window.addEventListener('cartUpdated', (e) => {
    console.log('Cart updated:', e.detail);
});

window.addEventListener('productSelected', (e) => {
    console.log('Product selected:', e.detail.product);
});
```

## Mobile Optimization

The components are fully responsive and include:
- Touch-friendly interactions
- Mobile sidebar navigation
- Optimized modal sizing
- Gesture support
- Performance optimizations

## Browser Compatibility

- Modern browsers (Chrome, Firefox, Safari, Edge)
- ES6+ features used
- Local storage required for persistence
- Touch events for mobile devices

## Future Enhancements

Possible extensions:
- User authentication
- Backend integration
- Payment processing
- Inventory management
- Analytics tracking
- SEO optimization

## Troubleshooting

### Common Issues
1. **Customizer not opening**: Check console for JavaScript errors
2. **Products not loading**: Verify image paths in `public/` folder
3. **Cart not persisting**: Check if local storage is enabled
4. **Mobile issues**: Clear browser cache and test in private mode

### Debug Mode
```javascript
// Enable debug logging
window.TissoVisonDebug = true;

// Check component status
TissoVisonDev.showState();
```

## Support

For development questions or issues:
1. Check the browser console for error messages
2. Verify all component files are loaded correctly
3. Test with the debug functions provided
4. Check local storage for saved configurations
