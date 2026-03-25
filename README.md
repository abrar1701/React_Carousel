# Ex05 Image Carousel
## Date:24-03-2026

## AIM
To create a Image Carousel using React 

## ALGORITHM
### STEP 1 Initial Setup:
Input: A list of images to display in the carousel.

Output: A component displaying the images with navigation controls (e.g., next/previous buttons).

### Step 2 State Management:
Use a state variable (currentIndex) to track the index of the current image displayed.

The carousel starts with the first image, so initialize currentIndex to 0.

### Step 3 Navigation Controls:
Next Image: When the "Next" button is clicked, increment currentIndex.

If currentIndex is at the end of the image list (last image), loop back to the first image using modulo:
currentIndex = (currentIndex + 1) % images.length;

Previous Image: When the "Previous" button is clicked, decrement currentIndex.

If currentIndex is at the beginning (first image), loop back to the last image:
currentIndex = (currentIndex - 1 + images.length) % images.length;

### Step 4 Displaying the Image:
The currentIndex determines which image is displayed.

Using the currentIndex, display the corresponding image from the images list.

### Step 5 Auto-Rotation:
Set an interval to automatically change the image after a set amount of time (e.g., 3 seconds).

Use setInterval to call the nextImage() function at regular intervals.

Clean up the interval when the component unmounts using clearInterval to prevent memory leaks.

## PROGRAM

### Carousel.jsx
```jsx
import React, { useState, useEffect } from "react";

const images = [
  "https://picsum.photos/id/1015/600/300",
  "https://picsum.photos/id/1016/600/300",
  "https://picsum.photos/id/1018/600/300",
];

export default function Carousel() {
  const [currentIndex, setCurrentIndex] = useState(0);

  const nextSlide = () => {
    setCurrentIndex((prevIndex) =>
      prevIndex === images.length - 1 ? 0 : prevIndex + 1,
    );
  };

  const prevSlide = () => {
    setCurrentIndex((prevIndex) =>
      prevIndex === 0 ? images.length - 1 : prevIndex - 1,
    );
  };

  useEffect(() => {
    const interval = setInterval(nextSlide, 3000);
    return () => clearInterval(interval);
  }, []);

  return (
    <div style={styles.container}>
      <button onClick={prevSlide} style={styles.button}>
        ❮
      </button>

      <img src={images[currentIndex]} alt="carousel" style={styles.image} />

      <button onClick={nextSlide} style={styles.button}>
        ❯
      </button>
    </div>
  );
}

const styles = {
  container: {
    display: "flex",
    alignItems: "center",
    justifyContent: "center",
    gap: "10px",
  },
  image: {
    width: "600px",
    height: "300px",
    objectFit: "cover",
    borderRadius: "10px",
  },
  button: {
    fontSize: "24px",
    cursor: "pointer",
    background: "none",
    border: "none",
  },
};
```

### main.jsx
```jsx
import { StrictMode } from "react";
import { createRoot } from "react-dom/client";
import "./index.css";
import Carousel from "./Caroseul";

createRoot(document.getElementById("root")).render(
  <StrictMode>
    <Carousel />
  </StrictMode>,
);
```

## OUTPUT
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/439ce51a-b8cc-4034-8f76-d54f0aa8721b" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/75e7789f-d461-43c4-935e-88efe6536444" />


## RESULT
The program for creating Image Carousel using React is executed successfully.
