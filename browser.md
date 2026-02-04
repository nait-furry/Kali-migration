How Browsers Find Site Images:

**Chrome Developer Tools** is the most direct way to view only images loaded by a website. Open the browser’s developer tools (F12 or right-click → Inspect), go to the **Network** tab, and reload the page. Use the **"Images" filter** or type `resource-type:image` in the filter box to display only image requests. This shows all images the site loaded, including those from CSS, JavaScript, or dynamically rendered content.

For **automated or bulk extraction**, tools like **wget**, **HTTrack**, or **Octoparse** can download entire websites, including all images. These tools can be configured to scrape only image assets, though they may require additional setup to avoid violating a site’s terms of service or triggering anti-bot measures like Cloudflare.

**Security note**: Browsers can load images from any domain, including those protected by session cookies, but **cross-origin image restrictions** prevent scripts from reading pixel data (e.g., via `canvas.getImageData()`) unless the server explicitly allows it via **CORS headers**. This protects user data even when images are loaded.

# Dowloading stuff to file:
You cannot directly pipe `console.log` output from the Chrome DevTools console to a file using shell-like redirection. However, you can capture the image sources and save them to a file using JavaScript in the console. 

### Solution
Use this code in the Chrome DevTools console to generate a downloadable file:

```javascript
const imgSources = Array.from(document.querySelectorAll('img')).map(img => img.src).join('\n');
const blob = new Blob([imgSources], { type: 'text/plain' });
const url = URL.createObjectURL(blob);
const a = document.createElement('a');
a.href = url;
a.download = 'image-links.txt';
a.click();
```

This script:
1. Collects all image `src` attributes
2. Joins them with newlines
3. Creates a downloadable text file
4. Automatically triggers the download 


