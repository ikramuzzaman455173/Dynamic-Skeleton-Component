### Dynamic Skeleton Component

This document provides an overview of a **dynamic skeleton component** designed to display loading placeholders in a variety of shapes and sizes. This component is reusable and customizable, making it suitable for different parts of your application like product cards, text blocks, and more.

---

### Table of Contents

1. **Component Overview**
2. **Props**
3. **CSS Setup**
4. **Usage Examples**
   - Product Card Skeleton
   - Text Content Skeleton
   - Skeleton Grid
5. **Dynamic Skeleton in Product List**
6. **Conclusion**

---

### 1. **Component Overview**

The `Skeleton` component is designed to provide a loading placeholder for different UI elements. It is a dynamic and flexible component, allowing you to customize the width, height, border radius, and other styles. This component is useful for keeping the layout intact while content is being loaded asynchronously.

#### Skeleton Component

```tsx
interface SkeletonProps {
  width?: string;
  height?: string;
  borderRadius?: string;
  className?: string;
}

const Skeleton: React.FC<SkeletonProps> = ({
  width = '100%',
  height = '20px',
  borderRadius = '4px',
  className = '',
}) => {
  return (
    <div
      className={`skeleton ${className}`}
      style={{ width, height, borderRadius }}
    ></div>
  );
};

export default Skeleton;
```

---

### 2. **Props**

| Prop Name    | Type   | Default Value | Description                                                       |
| ------------ | ------ | ------------- | ----------------------------------------------------------------- |
| `width`      | string | `"100%"`      | Sets the width of the skeleton placeholder.                       |
| `height`     | string | `"20px"`      | Sets the height of the skeleton placeholder.                      |
| `borderRadius`| string | `"4px"`       | Controls the border radius of the skeleton (for rounded elements). |
| `className`  | string | `""`          | Allows for additional styling or custom classes to be applied.     |

---

### 3. **CSS Setup**

The `skeleton` class is styled to provide a shimmering effect, simulating a loading state. You can modify this class to customize the appearance.

#### Skeleton CSS

```css
.skeleton {
  background-color: #e0e0e0;
  animation: pulse 1.5s infinite ease-in-out;
}

@keyframes pulse {
  0% {
    opacity: 1;
  }
  50% {
    opacity: 0.5;
  }
  100% {
    opacity: 1;
  }
}
```

- **`background-color`**: Defines the base color of the skeleton placeholder.
- **`pulse` animation**: Simulates a loading shimmer with a subtle opacity transition.

---

### 4. **Usage Examples**

#### **Example 1: Product Card Skeleton**

This example shows how the skeleton can be used to simulate loading for a product card.

```tsx
const ProductCardSkeleton: React.FC = () => {
  return (
    <div className="max-w-xs mx-auto bg-white shadow-md h-auto border p-3">
      <Skeleton width="100%" height="192px" borderRadius="8px" className="mt-5" /> {/* Image */}
      <div className="p-4 flex flex-col justify-between h-full mt-4">
        <Skeleton width="75%" height="20px" /> {/* Title */}
        <div className="flex justify-between mt-2">
          <Skeleton width="50px" height="20px" /> {/* Price */}
          <Skeleton width="40px" height="40px" borderRadius="50%" /> {/* Button */}
        </div>
        <Skeleton width="100px" height="16px" className="mt-2" /> {/* Rating */}
        <Skeleton width="40px" height="40px" borderRadius="50%" className="mt-5" /> {/* Cart button */}
      </div>
    </div>
  );
};
```

#### **Example 2: Text Content Skeleton**

The following example shows how to render a skeleton for loading text content, simulating paragraphs or headings.

```tsx
const TextContentSkeleton: React.FC = () => {
  return (
    <div>
      <Skeleton width="60%" height="24px" /> {/* Title */}
      <Skeleton width="100%" height="16px" className="mt-2" /> {/* Line of text */}
      <Skeleton width="90%" height="16px" className="mt-2" /> {/* Line of text */}
      <Skeleton width="85%" height="16px" className="mt-2" /> {/* Line of text */}
    </div>
  );
};
```

#### **Example 3: Skeleton Grid**

You can also use the `Skeleton` component to create a grid of placeholders, ideal for showing multiple items such as images or cards.

```tsx
const SkeletonGrid: React.FC = () => {
  return (
    <div className="grid grid-cols-2 gap-4">
      {[...Array(6)].map((_, index) => (
        <Skeleton key={index} width="100%" height="150px" borderRadius="8px" />
      ))}
    </div>
  );
};
```

---

### 5. **Dynamic Skeleton in Product List**

In real-world use cases, skeletons are often conditionally rendered based on loading state. Here’s an example of how to dynamically display skeletons in a product list:

```tsx
const ProductList: React.FC = ({ loading, products }) => {
  return (
    <div className="grid grid-cols-4 gap-4">
      {loading
        ? [...Array(8)].map((_, index) => <ProductCardSkeleton key={index} />)
        : products.map((product) => <ProductCard key={product.id} product={product} />)}
    </div>
  );
};
```

- **`loading`**: When `loading` is `true`, skeletons are shown. Otherwise, the actual product data is rendered.

---

### 6. **Conclusion**

The **dynamic skeleton component** is designed to be highly reusable and customizable across different parts of your application. By simply adjusting the width, height, and border radius, you can use the same skeleton component for various UI elements, such as images, text, buttons, and more. This approach ensures consistency and efficiency while handling loading states in your app.

