# Ex05 Image Carousel
## Date:05-11-25
## Name: Srikaran M
## Reg No: 212223040206

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
ImageCarousel.jsx
```
import React, { useState, useEffect } from "react";

function ImageCarousel({ images, interval = 3000 }) {
  const [currentIndex, setCurrentIndex] = useState(0);

  useEffect(() => {
    const timer = setInterval(() => {
      setCurrentIndex((prev) => (prev + 1) % images.length);
    }, interval);
    return () => clearInterval(timer);
  }, [images.length, interval]);

  const prevSlide = () => {
    setCurrentIndex((prev) => (prev === 0 ? images.length - 1 : prev - 1));
  };

  const nextSlide = () => {
    setCurrentIndex((prev) => (prev + 1) % images.length);
  };

  return (
    <div style={styles.carousel}>
      <button onClick={prevSlide} style={{ ...styles.button, left: "10px" }}>
        ❮
      </button>

      <img
        src={images[currentIndex]}
        alt={`Slide ${currentIndex + 1}`}
        style={styles.image}
      />

      <button onClick={nextSlide} style={{ ...styles.button, right: "10px" }}>
        ❯
      </button>

      <div style={styles.dots}>
        {images.map((_, index) => (
          <span
            key={index}
            style={{
              ...styles.dot,
              backgroundColor: index === currentIndex ? "#333" : "#bbb",
            }}
          />
        ))}
      </div>
    </div>
  );
}

const styles = {
  carousel: {
    position: "relative",
    width: "80%",
    maxWidth: "800px",
    margin: "20px auto",
    overflow: "hidden",
    borderRadius: "12px",
    boxShadow: "0 4px 20px rgba(0,0,0,0.2)",
    backgroundColor: "#fff",
  },
  image: {
    width: "100%",
    height: "auto",          // maintains aspect ratio
    maxHeight: "450px",      // limits image height
    objectFit: "contain",    // prevents zoom or crop
    borderRadius: "12px",
    imageRendering: "high-quality", // sharper display
  },
  button: {
    position: "absolute",
    top: "50%",
    transform: "translateY(-50%)",
    background: "rgba(0,0,0,0.5)",
    color: "#fff",
    border: "none",
    borderRadius: "50%",
    width: "40px",
    height: "40px",
    cursor: "pointer",
    fontSize: "20px",
    transition: "background 0.3s",
  },
  dots: {
    textAlign: "center",
    padding: "10px",
  },
  dot: {
    height: "12px",
    width: "12px",
    margin: "0 4px",
    display: "inline-block",
    borderRadius: "50%",
    transition: "background-color 0.3s",
  },
};

export default ImageCarousel;

```
App.jsx
```
import React from "react";
import ImageCarousel from "./ImageCarousel";

import img1 from "./assets/1.webp";
import img2 from "./assets/2.webp";
import img3 from "./assets/3.webp";

function App() {
  const images = [img1, img2, img3];

  return (
    <div style={{ textAlign: "center", padding: "20px" }}>
      <h1>React Image Carousel</h1>
      <ImageCarousel images={images} interval={3000} />
    </div>
  );
}

export default App;

```

## OUTPUT
<img width="1917" height="1079" alt="image" src="https://github.com/user-attachments/assets/2f3dca75-c4e6-49b3-8d17-c9f32d32046f" />
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/af30375a-26db-4799-9d3f-1d8bfec3bbcd" />
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/131c6306-be8c-4e47-8858-fb67ac6394ca" />


## RESULT
The program for creating Image Carousel using React is executed successfully.
