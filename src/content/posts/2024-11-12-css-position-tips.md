---
title: CSS Position Deep Dive
published: 2024-11-12
description: ''
image: ''
tags: [CSS, Web]
category: 'Front-end'
draft: false
lang: 'en'
---


When people first encounter web development, one of the biggest challenges is navigating the maze-like structure of HTML files and extensive CSS code. An analogy that might help make this clearer is to think of a webpage as an “unfurnished house.” HTML represents the various "furniture" pieces within the house, while CSS acts as the “interior designer,” responsible for defining the size, appearance, and arrangement of each piece within the space.

In web development, the first step in using CSS to style a website is determining the position of various elements on the page—this is **layout**！Let's start with layout.


# Get Started
The key concept we need to understand first is the CSS `position` property. This property forms the foundation of how we lay out web elements.

First, let’s create a set of nested HTML code:

```html
<div class="parent">
    <div class="baby"></div>
</div>
```

This structure gives us a **parent** container with a nested **baby** element inside.

Now let’s add some basic CSS to set up sizes and colors, making the elements easy to see:

```css
.parent {
    width: 500px;
    height: 500px;
    background-color: lightblue;
}

.baby {
    width: 200px;
    height: 200px;
    background-color: lightcoral;
}
```

Following this, with the CSS applied, the **parent** div appears as a 500x500px light blue box, and the **baby** div appears as a 200x200px light coral box inside it. This setup makes the nested structure clear and easy to visualize.

The generated webpage elements are shown below:

<figure>
    <img src="https://private-user-images.githubusercontent.com/44009421/385573199-27b79fed-500d-48db-98eb-367b90fc509e.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MzE0ODQxMzIsIm5iZiI6MTczMTQ4MzgzMiwicGF0aCI6Ii80NDAwOTQyMS8zODU1NzMxOTktMjdiNzlmZWQtNTAwZC00OGRiLTk4ZWItMzY3YjkwZmM1MDllLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDExMTMlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQxMTEzVDA3NDM1MlomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTdmOWFhY2ZmOGQyNDgxYTM5MmY2MGY1ZjdmZjhmMDYzMzcyMDUzYmVhZjA3ODY1ZmNlMGIwZjg3NDMxNDRhZjMmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.4Tcjfta5NgL1Uvbf6UrSbrJ3g6B1-mlBVQUPwdnMB0E" alt="pic-1">
    <figcaption><i>Image 1: Initial position of the baby element.</i></figcaption>
</figure>

# CSS Position
## Absolute Position

Let’s add the `position` property to the **baby** element along with other properties to center it within its layout:

```css
.parent {
    /* ... */
}

.baby {
    /* ... */
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}
```

We’ll notice that when the **baby** element's `position` is set to `absolute`, it does not center relative to the **parent** but instead centers within the entire webpage, as shown in the image.

<figure>
    <img src="https://private-user-images.githubusercontent.com/44009421/385578108-4003f981-106d-4fea-a108-a73f875af835.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MzE0ODQxMzIsIm5iZiI6MTczMTQ4MzgzMiwicGF0aCI6Ii80NDAwOTQyMS8zODU1NzgxMDgtNDAwM2Y5ODEtMTA2ZC00ZmVhLWExMDgtYTczZjg3NWFmODM1LnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDExMTMlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQxMTEzVDA3NDM1MlomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTQ4YzkwYmQxN2RiYzEwODQzM2U3ZTdlY2Q1OTFkMTI5OTA0ZWM1ZWQxMTY5MDMyMmJmYzM3ZGI2MTBlMTVmMjAmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.Mk6nwQElVsiLxykoxGjdjfWYyw01JTERTM8V3Aroiz0" alt="pic-2">
    <figcaption><i>Image 2: The baby element is centered relative to the viewport.</i></figcaption>
</figure>


**Why?** Because the **baby** element’s `position` is set to `absolute`, it searches for the nearest positioned ancestor to align with. However, since the **parent** element lacks any assigned `position` property, **baby** continues moving up the hierarchy to find one. With no positioned ancestor available, it defaults to aligning relative to the entire webpage (viewport).

## Relative position

Next, we’ll change the **baby** element’s `position` property to `relative`:

```css
.parent {
    /* ... */
}

.baby {
    /* ... */
    position: relative;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}
```

<figure>
    <img src="https://private-user-images.githubusercontent.com/44009421/385643620-09cd6dce-9a34-4fc2-b44b-73b1a3a57fcf.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MzE0ODM2NzAsIm5iZiI6MTczMTQ4MzM3MCwicGF0aCI6Ii80NDAwOTQyMS8zODU2NDM2MjAtMDljZDZkY2UtOWEzNC00ZmMyLWI0NGItNzNiMWEzYTU3ZmNmLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDExMTMlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQxMTEzVDA3MzYxMFomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTA5MmU0ZjY0YWU3YmFjMjBiOGY4Y2ExZDcyMmZmMmMzMTI1ZDkzODcwNWZmMGNlMTM2MWI1MTgyNzg1OTU5YzEmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.QintRyCQCVHDGqBXxQzyW2DjnBcZOXPJJRmNbDUoNNY" alt="pic-3">
    <figcaption><i>Image 3: The baby element appears centered relative to the parent element.</i></figcaption>
</figure>

As shown in the image below, the **baby** element appears centered within the **parent** element. This is because, with `position: relative`, the **baby** element’s offset uses its initial position as a reference point (see Image 1). The combination of `top` and `left` offsets with `transform` creates the visual effect of **baby** being centered within **parent**.

**Note!** When **parent** has no `position` property and **baby** is set to `relative` (with no other higher-level positioned ancestors in this example), **baby** uses its original position as the reference point (see Image 1). Although this approach achieves a centered look, it is not strictly centered relative to **parent** but rather a visual centering effect created by offset and transform adjustments.

## What Is Positioned Ancestor

Earlier in the article, the concept of a **positioned ancestor** was mentioned. So, what is a positioned ancestor? A positioned ancestor is the closest parent element within an element's hierarchy that has its `position` property set to any value other than `static`. In this case, if a child element has its `position` property set to `absolute` or `fixed`, it will use this ancestor as its reference point for positioning.

Now, we adjust the CSS for the **parent** and **baby** elements as follows:

```css
.parent {
    /* ... */
    position: relative;
}

.baby {
    /* ... */
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}
```
In this setup, the **baby** element is strictly positioned relative to the **parent** element.

<figure>
    <img src="https://private-user-images.githubusercontent.com/44009421/385666388-9c71525d-eaf6-414b-8139-571f77759f0d.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MzE0OTQ5NzksIm5iZiI6MTczMTQ5NDY3OSwicGF0aCI6Ii80NDAwOTQyMS8zODU2NjYzODgtOWM3MTUyNWQtZWFmNi00MTRiLTgxMzktNTcxZjc3NzU5ZjBkLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDExMTMlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQxMTEzVDEwNDQzOVomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTg4NGI0MmJmYWUzYjY5OGNjODE3MGJmMjUzMTAzNTNiNmVmZGQxMjQ3MjY2YjliNTY1NmMwMDJkNzY2NzM2ZmImWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.GEItRKrPLy0lpIyd6SYi0_73k8fN6aZrSDPQKAx6Nd0" alt="pic-4">
    <figcaption><i>Image 4: The baby element is strictly centered relative to the parent element.</i></figcaption>
</figure>

## Static Position

What is **static position**? by default, `static` is the default positioning mode. When an element does not have a `position` property specified, it defaults to `static` positioning.

Let's continue by modifying our existing CSS:

```css
.parent {
    /* ... */
    position: relative;
}

.baby {
    /* ... */
    position: static;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}
```

As shown in the image below, the **baby** element is no longer affected by the `top` and `left` properties. The reason **baby** shifts toward the top-left corner of the viewport is that, when set to `static`, it returns to its default position, which aligns with the top-left corner of the **parent**. However, the `transform` property still applies, causing **baby** to shift leftward on the x-axis and upward on the y-axis, resulting in its offset position.

<figure>
    <img src="https://private-user-images.githubusercontent.com/44009421/385676126-ae9d93ac-b18d-41a2-a35a-9ee4dee8d4e4.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MzE0OTQ5NzksIm5iZiI6MTczMTQ5NDY3OSwicGF0aCI6Ii80NDAwOTQyMS8zODU2NzYxMjYtYWU5ZDkzYWMtYjE4ZC00MWEyLWEzNWEtOWVlNGRlZThkNGU0LnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDExMTMlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQxMTEzVDEwNDQzOVomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTUzZDkwZGQ4ZDJjZTQ1YTJhOGU5N2VhODM3YTkyN2NiYWJlY2UwYjg3NDU0NGU5MjhiN2ZkY2MzMmFmZThhMmQmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.UTza4p9okYdlfLdPxd9VoTFKOnCuMHFGLCM5QxiVs5M" alt="pic-5">
    <figcaption><i>Image 5: Result of applying static positioning to the baby element.</i></figcaption>
</figure>

## Fixed Position

Before explaining the `fixed` property, set the `body` height to 10,000px. I know this value is a bit exaggerated 😜, but it ensures that the webpage can be scrolled regardless of screen size. Next, change the `position` property of the **baby** element to `fixed`:

```css
body {
    height: 10000px;
}

.parent {
    /* ... */
    position: absolute;
}

.baby {
    /* ... */
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}
```

Since **baby** now has `position: fixed`, it will no longer be positioned relative to **parent**. Instead, it will be positioned relative to the viewport. As shown in the animation below, when the webpage starts scrolling, the **baby** element maintains its position relative to the viewport.

<figure>
    <img src="https://private-user-images.githubusercontent.com/44009421/385688286-3e3a2eb3-db15-48f6-9560-8ec7fdbe9533.gif?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MzE0OTQ5NzksIm5iZiI6MTczMTQ5NDY3OSwicGF0aCI6Ii80NDAwOTQyMS8zODU2ODgyODYtM2UzYTJlYjMtZGIxNS00OGY2LTk1NjAtOGVjN2ZkYmU5NTMzLmdpZj9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDExMTMlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQxMTEzVDEwNDQzOVomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPWMwMjQ4YzgxMGZmYzliYjI3YmQ3ZjY5NzJhMGMzZTNmNGFhMDBiZmRhMWMzNDhhZTA4NjViOTI0ODI1NTgxZjgmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.oN7E9oNmB0vrmXJQpfK_RKyL-e3aZ4e8IjTr9Ar7FNU" alt="gif-1">
    <figcaption><i>Gif 1: The baby element remains fixed at the center of the viewport.</i></figcaption>
</figure>

## Sticky Position

First, set the height of the **parent** element to 1000px to make it easier to observe:

```css
.parent {
    width: 500px;
    height: 1000px; /* adjusted from 500px to 1000px */
    background-color: lightblue;
}
```

Next, change the `position` of the **baby** element to `sticky` and remove the `left` and `transform` properties to better observe and understand the effect:

```css
.parent {
    /* ... */
    position: absolute;
}

.baby {
    /* ... */
    position: sticky;
    top: 100px;
}
```

In this setup, `top: 100px` means that when the **baby** element is 100px away from the top of its scrolling container (in this case, **parent**), it will "stick" to that position, maintaining a fixed spot in the viewport.

<figure>
    <img src="https://private-user-images.githubusercontent.com/44009421/385715314-51e36ce0-57ea-4468-b58e-cad19af6529d.gif?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MzE0OTQ5NzksIm5iZiI6MTczMTQ5NDY3OSwicGF0aCI6Ii80NDAwOTQyMS8zODU3MTUzMTQtNTFlMzZjZTAtNTdlYS00NDY4LWI1OGUtY2FkMTlhZjY1MjlkLmdpZj9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDExMTMlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQxMTEzVDEwNDQzOVomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTIxNTU5NmU4OTBiZjI0MzdjMDE1M2M3M2YwYmI5MjRhZDdkOWYxMjc2ZWM3NzkzY2IyODViYjliMTRlZDQ3OWMmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.sLOVkBxvp90NxBdDDw8TNaKBQ2xp4iBAYCz-5aWPqJg" alt="gif-2">
    <figcaption><i>GIF 2: Animation demonstrating the sticky effect of the baby element.</i></figcaption>
</figure>

### Explanation of the Animation

In the animation, initially, the **baby** element stays within the **parent** element and remains fixed 100px from the top of the viewport. However, when the bottom edge of the **baby** element reaches the bottom edge of the **parent**, and as **parent** continues to scroll up, the **baby** element scrolls out of the viewport along with **parent**.

### Reasoning

This behavior occurs because the `sticky` positioning of the **baby** element only takes effect as long as it can maintain the `top: 100px` offset from its scrolling container (**parent**). When the **baby** element’s bottom edge meets the **parent**'s bottom boundary, it can no longer maintain a 100px distance from the top of **parent**. Consequently, as **parent** keeps scrolling, **baby** moves along with it and eventually scrolls out of the viewport.

It’s important to note that the **baby** element's `position` is still `sticky`; however, once it reaches the boundaries of its parent element, the sticky effect no longer applies.


# Summary

This article offers a practical overview of CSS positioning—covering static, relative, absolute, fixed, and sticky. Through examples and animations, it demonstrates how each positioning type affects an element’s placement within the viewport or relative to its parent.

- **Static**: The default positioning, following normal document flow.
- **Relative**: Offsets elements from their original location without disrupting flow.
- **Absolute**: Positions elements relative to the nearest positioned ancestor or viewport, removing them from document flow.
- **Fixed**: Keeps elements anchored to the viewport, ideal for persistent UI components.
- **Sticky**: Combines relative and fixed behavior, holding elements in place after scrolling to a specified offset.

This guide provides clear insights for mastering CSS positioning techniques in web development.