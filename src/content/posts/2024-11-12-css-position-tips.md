---
title: css position deep dive
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


# get started
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

# Position
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
    <figcaption><i>Image 2: Baby is centred relative to the web page.</i></figcaption>
</figure>


**Why?** Because the **baby** element’s `position` is set to `absolute`, it searches for the nearest positioned ancestor to align with. However, since the **parent** element lacks any assigned `position` property, **baby** continues moving up the hierarchy to find one. With no positioned ancestor available, it defaults to aligning relative to the entire webpage (viewport).

# Relative position

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
    <figcaption><i>Image 3: The baby looks centered relative to the parent.</i></figcaption>
</figure>

As shown in the image below, the **baby** element appears centered within the **parent** element. This is because, with `position: relative`, the **baby** element’s offset uses its initial position as a reference point (see Image 1). The combination of `top` and `left` offsets with `transform` creates the visual effect of **baby** being centered within **parent**.

**Note!** When **parent** has no `position` property and **baby** is set to `relative` (with no other higher-level positioned ancestors in this example), **baby** uses its original position as the reference point (see Image 1). Although this approach achieves a centered look, it is not strictly centered relative to **parent** but rather a visual centering effect created by offset and transform adjustments.

