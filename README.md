# Interactive HTML CV with High-Quality PDF Generator

## Project Overview

This project is a modern, responsive, single-page CV (Curriculum Vitae) created with a focus on high-quality presentation, both on-screen and in its downloaded PDF format. It is built with vanilla HTML, CSS, and JavaScript, and is designed to be a dynamic, professional, and easily customizable online resume.

The entire application runs client-side, requiring no backend or server. It's an excellent portfolio piece for demonstrating proficiency in front-end web technologies and creating a polished user experience. The primary goal is to provide a CV that not only looks good on the web but can be reliably converted into a perfectly formatted, crystal-clear, single-page PDF for professional use.

---

## Key Features

This CV comes packed with features designed for a professional and user-friendly experience:

#### 1. Crystal-Clear PDF Downloads

Generates a high-fidelity, single-page PDF of the CV that is perfect for printing or emailing.
* **Technical Implementation:** The blurriness issue common with other methods is solved by using the specialized `html2pdf.js` library. Unlike screenshot-based methods, this library directly interprets the DOM (Document Object Model) to create a vector-based PDF, ensuring text and elements remain perfectly sharp at any zoom level. The script is configured to render at **4x scale** and **300 DPI** for maximum quality and uses a lossless **PNG** format for any images.

#### 2. Guaranteed Single-Page Output

A "compact mode" is temporarily activated during PDF generation to slightly adjust spacing, ensuring the entire CV, including the footer, fits perfectly onto one A4 page without sacrificing quality.
* **Technical Implementation:** When the download button is clicked, a CSS class (`.pdf-export`) is added to the main container. This class triggers a set of more aggressive spacing and font-size rules, making the layout more compact. This modified layout is used only for the PDF generation and is removed immediately after, leaving the on-screen display unchanged.

#### 3. Interactive Profile Picture Uploader

Hover over the profile picture to reveal an upload button, allowing you to instantly change the photo on the fly.
* **Technical Implementation:** This feature uses the browser's native `FileReader` API. When a user selects a file, the JavaScript reads the image locally and converts it into a Base64 data URL. This URL is then set as the `src` for the `<img>` tag, updating the picture instantly without needing to upload it to a server.

#### 4. Modern & Responsive Design

A clean, two-column layout that looks great on all devices, from mobile phones to desktop monitors, achieved with flexible CSS layouts and media queries.

---

## File Structure

The entire project is self-contained within the `muhib CV.html` file, making it extremely portable. The file is organized as follows:

1.  **`<head>`**: Contains metadata, the title, and links to external resources like the Font Awesome icon library and the `html2pdf.js` script.
2.  **`<style>`**: Holds all the CSS for the project, including:
    * Global styles and CSS variables for easy theme customization.
    * Layout rules for the two-column design.
    * The special `.pdf-export` styles for the compact PDF layout.
    * Responsive design adjustments using media queries.
3.  **`<body>`**: The main HTML content of the CV, semantically structured into sections.
4.  **`<script>`**: The JavaScript logic at the bottom of the body, which handles the two main interactive features: PDF generation and the profile picture uploader.

---

## Customization Guide

This CV is designed to be easily personalized.

* **Editing Content:** All text (names, job titles, experience, etc.) can be changed by directly editing the text within the HTML tags in the `muhib CV.html` file.
* **Changing Colors:** The main color scheme can be adjusted by changing the CSS variables at the top of the `<style>` section.
    ```css
    :root {
        --primary-color: #3498db; /* Changes the main accent color (blue) */
        --secondary-color: #2c3e50; /* Changes the dark sidebar color */
    }
    ```
* **Adjusting Skill Levels:** The animated skill bars can be updated by changing the `--skill-level` inline variable for each skill.
    ```html
    <li>Automation<div class="skill-bar"><div class="skill-level" style="--skill-level: 85%;"></div></div></li>
    ```

---

## Technical Deep Dive

The interactivity is powered by two main JavaScript functions:

#### PDF Generation

The `downloadBtn` event listener orchestrates the entire PDF creation process:
1.  **State Management:** The button's text is changed to "Generating..." and it's disabled to prevent multiple clicks.
2.  **Compact Mode:** The `.pdf-export` class is added to the main CV container. This is the key to ensuring the single-page output.
3.  **Configuration:** An `options` object is defined for `html2pdf.js`, specifying the filename, margins, and high-quality rendering settings (`scale: 4`, `dpi: 300`, `image: { type: 'png' }`).
4.  **Execution:** The `html2pdf().from(element).set(options).save()` chain is called. This is an asynchronous operation.
5.  **Cleanup:** The `.then()` and `.catch()` promises ensure that, whether the generation succeeds or fails, the `.pdf-export` class is removed and the download button is restored to its original state.

#### Profile Picture Uploader

The `upload-photo` input has its own event listener:
1.  **Event Trigger:** It listens for a `change` event, which fires when the user selects a file.
2.  **File Reading:** It creates a new `FileReader` object.
3.  **Data Conversion:** The `reader.readAsDataURL(file)` method reads the image file and converts it into a Base64-encoded string.
4.  **Display Update:** The `reader.onload` function is triggered when the conversion is complete. It sets the `src` attribute of the profile `<img>` tag to the new Base64 string, causing the browser to display the selected image.

---

## Technologies Used

* **HTML5:** For the structure and content of the CV.
* **CSS3:** For all styling, including the layout, colors, animations, and responsive design.
* **JavaScript (ES6):** For the interactive functionality.
* **[Font Awesome](https://fontawesome.com/):** For the icons used throughout the CV.
