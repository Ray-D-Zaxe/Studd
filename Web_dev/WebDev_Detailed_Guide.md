# Web Development Master's Syllabus - Final Exam Study Guide
## With Detailed Code Explanations

---

## UNIT I: Web Terminologies, HTML5, CSS3, and Bootstrap

### **Web Terminologies**

#### **Internet**
- **Definition**: Global system of interconnected networks using TCP/IP protocol for data transmission
- **Function**: Enables communication between computers worldwide
- **Key Point**: Internet is the infrastructure, Web is a service built on it
- **Example**: Email, FTP, HTTPS all run on the Internet

#### **World Wide Web (WWW)**
- **Definition**: System of interlinked documents accessed via the Internet using HTTP/HTTPS
- **Components**: URLs, HTTP protocol, web browsers, web servers
- **Created By**: Tim Berners-Lee (1989)
- **Example**: www.google.com is a web resource

#### **Web Browser**
- **Definition**: Client-side software that renders and displays web pages
- **Function**: 
  - Parses HTML, CSS, and JavaScript
  - Requests resources from web servers
  - Renders multimedia content
- **Examples**: Chrome, Firefox, Safari, Edge
- **Key Browsers' Request Flow**: Browser → URL → DNS Resolution → Web Server → Response → Rendering

#### **How Web Browser Communicates with Web Server**
1. **User enters URL** in address bar
2. **DNS Lookup**: Browser resolves domain name to IP address
3. **TCP Connection**: Browser establishes TCP connection (three-way handshake)
4. **HTTP Request**: Browser sends HTTP request to server
5. **Server Processing**: Web server processes request
6. **HTTP Response**: Server sends back response (HTML, CSS, JS, media)
7. **Rendering**: Browser renders the page
8. **Connection Close**: TCP connection closes (or kept alive)

**Example HTTP Request-Response Cycle**:
```
GET /index.html HTTP/1.1
Host: www.example.com

HTTP/1.1 200 OK
Content-Type: text/html
Content-Length: 1234

<!DOCTYPE html>
<html>...</html>
```

**Code Explanation**:
- `GET`: HTTP method requesting to retrieve data (alternative: POST for sending data)
- `/index.html`: Path to resource on server
- `HTTP/1.1`: Protocol version
- `Host: www.example.com`: Server address being requested
- `HTTP/1.1 200 OK`: Response indicating success (200 = OK status code)
- `Content-Type: text/html`: Tells browser to expect HTML content
- `Content-Length: 1234`: Size of response body in bytes

#### **Web Server**
- **Definition**: Server software that receives HTTP requests and sends HTTP responses
- **Function**: Hosts web pages, processes requests, manages resources
- **Examples**: Apache, Nginx, IIS (Internet Information Services)
- **Response**: Serves static files (HTML, CSS, JS) or generates dynamic content

#### **Uniform Resource Locator (URL)**
- **Definition**: Web address identifying location of resource
- **Structure**: `protocol://subdomain.domain.tld/path?query#fragment`
- **Example**: `https://www.example.com:8080/products?category=electronics#reviews`
  - Protocol: `https` (secure connection)
  - Subdomain: `www` (often represents main website)
  - Domain: `example.com` (site name)
  - Port: `8080` (communication endpoint; 443 is default for HTTPS)
  - Path: `/products` (directory/resource location)
  - Query: `category=electronics` (parameters passed to server)
  - Fragment: `reviews` (jump to section on page; client-side only)

#### **HTTPS (Hypertext Transfer Protocol Secure)**
- **Definition**: Secure version of HTTP using SSL/TLS encryption
- **Key Features**:
  - End-to-end encryption (data unreadable if intercepted)
  - SSL certificate verification (confirms website authenticity)
  - Data integrity (detects tampering)
  - Authentication (verifies you're on real website)
- **Example**: Banking websites use HTTPS to protect financial data
- **Status Code**: Green padlock indicates secure connection
- **Port**: Default port 443 (vs HTTP port 80)

---

### **HTML5 Introduction**

#### **Structure of HTML5 Program**
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Page Title</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <header>
        <nav>Navigation Menu</nav>
    </header>
    <main>
        <article>
            <h1>Article Title</h1>
            <p>Content here</p>
        </article>
    </main>
    <footer>
        <p>&copy; 2024 Company Name</p>
    </footer>
    <script src="script.js"></script>
</body>
</html>
```

**How It Works - General Overview**:
The HTML5 document structure defines a complete web page layout. The browser reads this top-to-bottom, loading resources (CSS, JavaScript) and rendering the content. The structure separates metadata (head) from visible content (body), making it organized and search-engine friendly.

**Component Breakdown**:
- `<!DOCTYPE html>`: Declaration telling browser this is HTML5 (latest standard); must be first line; helps ensure consistent rendering
- `<html lang="en">`: Root element wrapping entire page; `lang="en"` specifies language for accessibility (screen readers) and SEO
- `<head>`: Container for metadata (invisible to users); includes character encoding, viewport settings, page title, external styles, scripts
- `<meta charset="UTF-8">`: Specifies character encoding (UTF-8 supports all languages and special characters worldwide)
- `<meta name="viewport" ...>`: Makes page responsive on mobile devices; sets viewport width to device width and initial zoom level
- `<title>`: Text appearing in browser tab and search results; critical for SEO and user navigation
- `<link rel="stylesheet" ...>`: Imports external CSS file for styling; `rel="stylesheet"` indicates relationship type
- `<body>`: Contains all visible content that users see and interact with
- `<header>`: Semantic element representing introductory content (logo, title, navigation)
- `<nav>`: Semantic element containing navigation links
- `<main>`: Semantic element for main content (improves accessibility and SEO)
- `<article>`: Semantic element for self-contained content (blog post, news article)
- `<footer>`: Semantic element for footer content (copyright, links, contact)
- `<script src="script.js">`: Loads external JavaScript at end of body (better performance than head)

---

#### **Heading Styles**
```html
<h1>Main Heading</h1>    <!-- Largest, typically one per page -->
<h2>Subheading</h2>
<h3>Sub-subheading</h3>
<h4>Level 4 Heading</h4>
<h5>Level 5 Heading</h5>
<h6>Minor Heading</h6>    <!-- Smallest -->
```

**How It Works**:
- Headings create hierarchy in document
- `<h1>` is most important (should appear once per page for SEO)
- Each level down is less important
- Screen readers use these to navigate; search engines use them to understand content structure
- CSS can override default sizes but semantic importance remains

**Best Practice**: Use headings hierarchically; don't skip levels (h1 → h2, not h1 → h3)

---

#### **Text Styles**
```html
<strong>Bold text (important)</strong>
<b>Bold text (visual)</b>
<em>Emphasized text (italic)</em>
<i>Italic text (visual)</i>
<mark>Highlighted text</mark>
<small>Small text</small>
<del>Deleted text</del>
<ins>Inserted text</ins>
<sub>Subscript text</sub>
<sup>Superscript text</sup>
```

**Code Explanation**:
- `<strong>`: Semantic emphasis (screen readers emphasize differently; indicates importance)
- `<b>`: Visual bold only (no semantic meaning; use `<strong>` when meaning matters)
- `<em>`: Semantic emphasis with stress (screen readers change tone; usually italic)
- `<i>`: Visual italic only (for alternative voice, technical terms; no semantic weight)
- `<mark>`: Highlights text as relevant (yellow background by default)
- `<small>`: Smaller text (copyright, disclaimers)
- `<del>`: Deleted/struck-through text (shows removed content)
- `<ins>`: Inserted text (shows added content)
- `<sub>`: Subscript (below baseline, smaller; for formulas like H₂O)
- `<sup>`: Superscript (above baseline, smaller; for exponents like x²)

---

#### **Lists**

**Ordered Lists**:
```html
<ol type="1">  <!-- 1, a, A, i, I -->
    <li>First item</li>
    <li>Second item</li>
    <li>Third item</li>
</ol>
```

**How It Works**:
- `<ol>`: Ordered list container (numbered sequentially)
- `type="1"`: Numbering style (1=numbers, a=lowercase letters, A=uppercase, i=lowercase roman, I=uppercase roman)
- `<li>`: List item (each item is numbered automatically)
- Browser auto-generates numbers; if HTML changes, numbers update automatically

---

**Unordered Lists**:
```html
<ul style="list-style-type: disc">  <!-- disc, circle, square, none -->
    <li>Item one</li>
    <li>Item two</li>
    <li>Item three</li>
</ul>
```

**How It Works**:
- `<ul>`: Unordered list container (bullet points, no sequence)
- `style="list-style-type: disc"`: Changes bullet style (disc=solid circle, circle=hollow, square=square, none=no bullet)
- `<li>`: List items get bullet points
- Better for non-sequential content

---

**Definition Lists**:
```html
<dl>
    <dt>HTML</dt>
    <dd>HyperText Markup Language - structure of web pages</dd>
    <dt>CSS</dt>
    <dd>Cascading Style Sheets - styling web pages</dd>
</dl>
```

**How It Works**:
- `<dl>`: Definition list container (for term-definition pairs)
- `<dt>`: Definition term (the word being defined)
- `<dd>`: Definition data (the explanation; auto-indented)
- Perfect for glossaries, key-value pairs, metadata

---

**Nested Lists**:
```html
<ul>
    <li>Web Technologies
        <ul>
            <li>Frontend</li>
            <li>Backend</li>
        </ul>
    </li>
</ul>
```

**How It Works**:
- Lists can contain other lists inside `<li>` elements
- Creates hierarchy and structure
- Each nested list is indented further
- Used for multi-level navigation, categorized content

---

#### **Images**
```html
<!-- Basic Image -->
<img src="image.jpg" alt="Description of image" width="300" height="200">

<!-- Image with Link -->
<a href="page.html">
    <img src="thumbnail.jpg" alt="Link description">
</a>

<!-- Responsive Image -->
<picture>
    <source media="(max-width: 768px)" srcset="mobile.jpg">
    <source media="(min-width: 769px)" srcset="desktop.jpg">
    <img src="default.jpg" alt="Responsive image">
</picture>

<!-- Image Map -->
<img src="shapes.jpg" usemap="#shapemap" alt="Shapes">
<map name="shapemap">
    <area shape="circle" coords="100,100,50" href="circle.html" alt="Circle">
    <area shape="rect" coords="200,100,400,200" href="rect.html" alt="Rectangle">
</map>
```

**Code Explanation**:

**Basic Image**:
- `<img>`: Self-closing tag that embeds image
- `src="image.jpg"`: Path to image file (required; can be relative or absolute URL)
- `alt="Description"`: Alternative text if image fails to load; read by screen readers; crucial for accessibility and SEO
- `width="300" height="200"`: Dimensions in pixels; reserves space so page doesn't shift when image loads

**Image with Link**:
- Wrapping `<img>` in `<a>` makes image clickable
- Clicking image navigates to linked page

**Responsive Image**:
- `<picture>`: Container that selects appropriate image based on conditions
- `<source media="..."`: Media query defining when this source applies
- `(max-width: 768px)`: Applies on screens 768px or smaller (mobile)
- `srcset="mobile.jpg"`: Image file to use for this condition
- Fallback `<img>`: Used if no source matches or browser doesn't support picture
- Saves bandwidth on mobile by serving smaller images

**Image Map**:
- `usemap="#shapemap"`: Links image to map with id "shapemap"
- `<map name="shapemap">`: Defines clickable regions on image
- `<area>`: Individual clickable area with coordinates
- `shape="circle" coords="100,100,50"`: Circle centered at (100,100) with radius 50
- `shape="rect" coords="200,100,400,200"`: Rectangle from (200,100) to (400,200)
- `href="circle.html"`: Where clicking that area navigates

---

#### **Tables**
```html
<table border="1">
    <caption>Student Grades</caption>
    <thead>
        <tr>
            <th>Roll No</th>
            <th>Name</th>
            <th>Grade</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>101</td>
            <td>John</td>
            <td>A</td>
        </tr>
        <tr>
            <td>102</td>
            <td>Jane</td>
            <td>A+</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <th>Total</th>
            <td colspan="2">2 students</td>
        </tr>
    </tfoot>
</table>
```

**How It Works - General Overview**:
Tables organize data in rows and columns. The browser reads the structure: header row defines column meanings, body rows contain data, footer row contains summary information. This semantic structure helps screen readers interpret data correctly.

**Component Breakdown**:
- `<table>`: Container for entire table; `border="1"` adds visible borders
- `<caption>`: Title/description of table (appears above; helpful for accessibility)
- `<thead>`: Table header section (first row typically); semantic grouping
- `<tr>`: Table row (one horizontal line of data)
- `<th>`: Table header cell (bold and centered by default; for column/row labels)
- `<tbody>`: Table body section (main data rows); semantic grouping
- `<td>`: Table data cell (regular cells containing data)
- `<tfoot>`: Table footer section (summary rows like totals)
- `colspan="2"`: Makes this cell span 2 columns horizontally
- `rowspan="2"`: Makes cell span 2 rows vertically

**Table Attributes**:
- `border="1"`: Add border
- `cellpadding="10"`: Space inside cells
- `cellspacing="5"`: Space between cells

---

#### **Multimedia**
```html
<!-- Audio Tag -->
<audio controls>
    <source src="audio.mp3" type="audio/mpeg">
    <source src="audio.wav" type="audio/wav">
    Your browser does not support audio tag
</audio>

<!-- Video Tag -->
<video width="400" height="300" controls poster="thumbnail.jpg">
    <source src="video.mp4" type="video/mp4">
    <source src="video.webm" type="video/webm">
    Your browser does not support video tag
</video>

<!-- Iframe (embedded content) -->
<iframe src="https://www.youtube.com/embed/dQw4w9WgXcQ" 
        width="560" height="315"></iframe>

<!-- Embedded SVG -->
<svg width="100" height="100">
    <circle cx="50" cy="50" r="40" fill="blue"></circle>
</svg>

<!-- Canvas for Graphics -->
<canvas id="myCanvas" width="200" height="200"></canvas>
<script>
    const canvas = document.getElementById('myCanvas');
    const ctx = canvas.getContext('2d');
    ctx.fillStyle = 'red';
    ctx.fillRect(10, 10, 150, 100);
</script>
```

**Code Explanation**:

**Audio Tag**:
- `<audio>`: HTML5 native audio player
- `controls`: Shows play/pause buttons, volume control
- `<source>`: Different file formats for browser compatibility
- `type="audio/mpeg"`: MIME type helps browser identify format
- Fallback text shown if browser doesn't support audio
- Why multiple sources? Different browsers support different formats (MP3, WAV, OGG)

**Video Tag**:
- `<video>`: HTML5 native video player
- `width="400" height="300"`: Video dimensions
- `controls`: Shows play/pause, seek bar, volume
- `poster="thumbnail.jpg"`: Image shown before video plays
- Multiple sources provide compatibility
- Similar fallback for older browsers

**Iframe**:
- `<iframe>`: Inline frame embedding external content
- `src="URL"`: Source of embedded content (YouTube video in example)
- `width="560" height="315"`: Dimensions of embedded content
- Used for embedding maps, videos, external pages
- Has its own separate window/document context

**SVG (Scalable Vector Graphics)**:
- `<svg>`: Container for vector graphics
- `width="100" height="100"`: Dimensions in pixels
- `<circle>`: SVG element drawing circle
- `cx="50" cy="50"`: Center coordinates
- `r="40"`: Radius
- `fill="blue"`: Color
- Advantage: Scales without quality loss; can be styled with CSS

**Canvas**:
- `<canvas>`: Container for pixel-based graphics drawn with JavaScript
- `id="myCanvas"`: Reference for JavaScript to access canvas
- `width="200" height="200"`: Canvas dimensions
- `document.getElementById()`: JavaScript gets canvas element
- `getContext('2d')`: Gets 2D drawing context
- `fillStyle = 'red'`: Sets fill color
- `fillRect(10, 10, 150, 100)`: Draws filled rectangle at (10,10) with width 150, height 100
- Difference from SVG: Canvas is pixel-based (rasterized); less scalable but more flexible for animations

---

#### **Graphics**
```html
<!-- SVG Graphics (Scalable Vector Graphics) -->
<svg width="200" height="200">
    <!-- Rectangle -->
    <rect x="10" y="10" width="100" height="50" fill="blue"></rect>
    
    <!-- Circle -->
    <circle cx="150" cy="50" r="30" fill="red"></circle>
    
    <!-- Line -->
    <line x1="0" y1="0" x2="200" y2="200" stroke="black" stroke-width="2"></line>
    
    <!-- Polygon -->
    <polygon points="100,10 40,198 190,78" fill="green"></polygon>
    
    <!-- Text -->
    <text x="10" y="30" fill="white">SVG Text</text>
</svg>

<!-- Canvas Graphics (using JavaScript) -->
<canvas id="canvas" width="400" height="300"></canvas>
<script>
    const canvas = document.getElementById('canvas');
    const ctx = canvas.getContext('2d');
    
    // Draw rectangle
    ctx.fillStyle = 'blue';
    ctx.fillRect(50, 50, 100, 75);
    
    // Draw circle
    ctx.fillStyle = 'red';
    ctx.beginPath();
    ctx.arc(200, 100, 50, 0, Math.PI * 2);
    ctx.fill();
    
    // Draw text
    ctx.fillStyle = 'black';
    ctx.font = '20px Arial';
    ctx.fillText('Canvas Text', 50, 250);
</script>
```

**SVG Code Explanation**:
- `<svg>`: SVG container (vector-based, scalable)
- `<rect>`: Rectangle shape; x, y (position), width, height
- `<circle>`: Circle; cx, cy (center), r (radius)
- `<line>`: Line; x1, y1 (start), x2, y2 (end), stroke (color), stroke-width (thickness)
- `<polygon>`: Multiple connected points; points formatted as "x1,y1 x2,y2 x3,y3"
- `<text>`: Renders text; x, y (position)
- All shapes can be styled with fill, stroke, opacity

**Canvas Code Explanation**:
- `const canvas = ...`: Gets canvas element reference
- `getContext('2d')`: Gets 2D context for drawing (3d not shown here)
- `ctx.fillStyle = 'blue'`: Sets fill color (applies to next shapes)
- `ctx.fillRect(50, 50, 100, 75)`: Draws filled rectangle at (50,50), 100px wide, 75px tall
- `ctx.beginPath()`: Starts new path (needed for complex shapes)
- `ctx.arc()`: Draws arc/circle; parameters: centerX, centerY, radius, startAngle, endAngle
- `Math.PI * 2`: 2π radians = full circle (0 to 2π)
- `ctx.fill()`: Fills the path with current fillStyle
- `ctx.font = '20px Arial'`: Sets font for text
- `ctx.fillText()`: Draws text at specified position

**When to Use Which**:
- **SVG**: Icons, logos, diagrams, animations (resolution-independent, can be styled like HTML)
- **Canvas**: Games, real-time animations, image manipulation (more control, better performance for complex drawings)

---

#### **Forms**
```html
<form action="process.php" method="POST">
    <!-- Text Input -->
    <label for="username">Username:</label>
    <input type="text" id="username" name="username" required>
    
    <!-- Email Input -->
    <label for="email">Email:</label>
    <input type="email" id="email" name="email">
    
    <!-- Password Input -->
    <label for="password">Password:</label>
    <input type="password" id="password" name="password">
    
    <!-- Number Input -->
    <label for="age">Age:</label>
    <input type="number" id="age" name="age" min="18" max="100">
    
    <!-- Date Input -->
    <label for="dob">Date of Birth:</label>
    <input type="date" id="dob" name="dob">
    
    <!-- Radio Buttons -->
    <label>Gender:</label>
    <input type="radio" name="gender" value="male"> Male
    <input type="radio" name="gender" value="female"> Female
    
    <!-- Checkboxes -->
    <label>Skills:</label>
    <input type="checkbox" name="skills" value="html"> HTML
    <input type="checkbox" name="skills" value="css"> CSS
    <input type="checkbox" name="skills" value="js"> JavaScript
    
    <!-- Textarea -->
    <label for="message">Message:</label>
    <textarea id="message" name="message" rows="5" cols="40"></textarea>
    
    <!-- Dropdown/Select -->
    <label for="country">Country:</label>
    <select id="country" name="country">
        <option value="">Select Country</option>
        <option value="india">India</option>
        <option value="usa">USA</option>
        <option value="uk">UK</option>
    </select>
    
    <!-- Submit Button -->
    <button type="submit">Submit</button>
    <button type="reset">Reset</button>
    <button type="button">Cancel</button>
</form>
```

**How It Works - General Overview**:
Form collects user input and sends it to server (action URL) using specified method. Each input element has a name (key) that becomes part of data sent. Browser validates before sending if validation attributes present.

**Component Breakdown**:
- `<form>`: Container for form elements
  - `action="process.php"`: URL where form data is sent
  - `method="POST"`: HTTP method (POST for sensitive data, GET for queries)
  
- `<label for="username">`: Text label linked to input with matching id (improves accessibility and clickability)

- **Text Input**: `<input type="text">` - Single-line text field
  - `id="username"`: Unique identifier (matches label's for attribute)
  - `name="username"`: Field name sent to server (key in key-value pair)
  - `required`: Browser prevents submission if empty

- **Email Input**: `<input type="email">` - Email validation built-in
  
- **Password Input**: `<input type="password">` - Characters shown as dots for security

- **Number Input**: `<input type="number">`
  - `min="18" max="100"`: Restricts range (browser shows spinner buttons)

- **Date Input**: `<input type="date">` - Calendar picker in modern browsers

- **Radio Buttons**: `<input type="radio">`
  - `name="gender"`: Same name groups options (only one can be selected)
  - `value="male"`: Data sent if selected
  - User sees label text, server gets value

- **Checkboxes**: `<input type="checkbox">`
  - Different names or same name with array notation: `name="skills[]"`
  - Multiple selections allowed (unlike radio)
  - Only checked boxes send data

- **Textarea**: `<textarea>` - Multi-line text input
  - `rows="5" cols="40"`: Visible dimensions
  - Good for comments, messages

- **Select/Dropdown**: `<select>`
  - `<option value="">`: Each option is choice
  - First option often blank for "please select"
  - Only selected option sends data

- **Buttons**:
  - `type="submit"`: Sends form data
  - `type="reset"`: Clears all form fields
  - `type="button"`: Custom action (needs JavaScript)

---

#### **Form Validation**
```html
<!-- HTML5 Built-in Validation -->
<form>
    <input type="email" required placeholder="Enter valid email">
    <input type="number" min="0" max="100" required>
    <input type="text" pattern="[A-Za-z]+" title="Only letters allowed">
    <input type="text" minlength="5" maxlength="10">
    <input type="url" required>
    <button type="submit">Submit</button>
</form>
```

**Code Explanation**:
- `required`: Browser prevents submission if field is empty; error message shown
- `type="email"`: Browser validates email format (must contain @ and domain)
- `type="number"`: Only numbers accepted; `min="0" max="100"` restricts range
- `pattern="[A-Za-z]+"`: Regular expression; only uppercase/lowercase letters allowed
  - `[A-Za-z]` = any letter
  - `+` = one or more
  - If pattern doesn't match, submission blocked
- `title="Only letters allowed"`: Message shown when pattern fails
- `minlength="5" maxlength="10"`: Text length must be 5-10 characters
- `type="url"`: Validates URL format (must be valid web address)

**How It Works**:
- Validation happens client-side (in browser) before sending to server
- Browser shows error messages for invalid fields
- Prevents unnecessary server requests
- User gets immediate feedback
- Server-side validation still needed for security (client-side can be bypassed)

---

### **CSS 3.0**

#### **CSS Concepts and Properties**

**Selectors**:
```css
/* Universal Selector - Targets ALL elements */
* { margin: 0; padding: 0; }

/* Element Selector - Targets by HTML tag name */
p { color: blue; }

/* Class Selector - Targets elements with specific class (reusable) */
.highlight { background-color: yellow; }

/* ID Selector - Targets element with specific ID (unique, use rarely) */
#header { background-color: navy; }

/* Attribute Selector - Targets by HTML attribute value */
input[type="email"] { border: 2px solid blue; }

/* Pseudo-class - Targets element in specific state */
a:hover { color: red; }           /* When user hovers over link */
a:visited { color: purple; }      /* Link already visited */
li:first-child { font-weight: bold; } /* First li in parent */

/* Pseudo-element - Targets part of element */
p::first-letter { font-size: 24px; }  /* First letter of paragraph */
p::first-line { font-weight: bold; }  /* First line of paragraph */

/* Combinators - Select elements based on relationship */
div > p { } /* Direct child: p directly inside div */
div p { }   /* Descendant: p anywhere inside div */
h1 + p { }  /* Adjacent sibling: p immediately after h1 */
h1 ~ p { }  /* General sibling: p after h1, same parent */
```

**How Selectors Work**:
- Browser reads CSS rules and applies to matching elements
- More specific selectors override general ones (specificity rules)
- Order matters: later rules override earlier ones (cascade)

---

**Border Properties**:
```css
.box {
    /* All borders at once */
    border: 2px solid #333;
    
    /* Individual properties */
    border-width: 2px;
    border-style: solid; /* solid, dashed, dotted, double, groove, ridge, inset, outset */
    border-color: #333;
    
    /* Rounded corners */
    border-radius: 10px;
    border-top-left-radius: 15px;  /* Individual corner */
    
    /* Shadow behind border */
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    /* Format: offsetX offsetY blurRadius color */
}
```

**Code Explanation**:
- `border: 2px solid #333`: Shorthand (width, style, color)
  - `2px`: Border thickness
  - `solid`: Border appearance (line type)
  - `#333`: Border color (dark gray)
- `border-radius: 10px`: Makes corners rounded (10px curve)
- `box-shadow: 0 4px 6px rgba(0,0,0,0.1)`:
  - `0`: Horizontal offset (0 = centered)
  - `4px`: Vertical offset (4px down)
  - `6px`: Blur radius (softer shadow)
  - `rgba(0,0,0,0.1)`: Black color at 10% opacity (semi-transparent)

---

**Background Properties**:
```css
.background {
    background-color: #f0f0f0;  /* Solid color behind element */
    background-image: url('image.jpg');  /* Image as background */
    background-repeat: no-repeat; /* no-repeat, repeat, repeat-x, repeat-y */
    background-position: center top;  /* Where image appears */
    background-size: cover; /* cover, contain, 100px 200px */
    background-attachment: fixed;  /* fixed, scroll */
    
    /* Shorthand combining all */
    background: #f0f0f0 url('image.jpg') no-repeat center fixed;
}
```

**Code Explanation**:
- `background-color`: Fallback color shown behind image
- `background-image: url()`: Path to image file
- `background-repeat`:
  - `no-repeat`: Image shown once
  - `repeat`: Tiles image across element
  - `repeat-x`: Tiles horizontally only
  - `repeat-y`: Tiles vertically only
- `background-position: center top`:
  - First value: horizontal (left, center, right, or pixel)
  - Second value: vertical (top, center, bottom, or pixel)
- `background-size`:
  - `cover`: Image scales to cover entire element (may crop)
  - `contain`: Image scales to fit inside (no crop, may have gaps)
  - `100px 200px`: Explicit dimensions
- `background-attachment: fixed`: Image stays fixed when scrolling (parallax effect)

---

**Font Properties**:
```css
.text {
    font-family: 'Arial', sans-serif;  /* Primary font, fallback fonts */
    font-size: 16px;  /* Base text size */
    font-weight: 400; /* 100-900, bold, normal */
    font-style: italic; /* normal, italic, oblique */
    line-height: 1.5;  /* Space between lines (1.5 = 150% of font size) */
    letter-spacing: 2px;  /* Space between letters */
    text-align: center; /* left, right, justify, center */
    text-decoration: underline; /* none, underline, overline, line-through */
    text-transform: uppercase; /* lowercase, uppercase, capitalize */
    text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);  /* Shadow under text */
}
```

**Code Explanation**:
- `font-family: 'Arial', sans-serif`:
  - Lists fonts in preference order (browser uses first available)
  - 'Arial' = specific font
  - `sans-serif` = generic fallback if Arial not available
- `font-size: 16px`: Size of text (16px typical for body text)
- `font-weight: 400`: Thickness (400=normal, 700=bold, lighter/bolder for relative)
- `line-height: 1.5`: Space between lines (1.5 = line height is 1.5× font size)
- `letter-spacing: 2px`: Gap between letters (negative values squeeze)
- `text-align`:
  - `center`: Centered
  - `left`: Left-aligned
  - `right`: Right-aligned
  - `justify`: Aligned to both edges
- `text-decoration: underline`: Line under/over/through text
- `text-transform`:
  - `uppercase`: ALL CAPS
  - `lowercase`: all lowercase
  - `capitalize`: First Letter Of Each Word
- `text-shadow: 2px 2px 4px rgba(0,0,0,0.5)`:
  - `2px 2px`: Offset right and down
  - `4px`: Blur
  - Color with opacity

---

**Text Effects**:
```css
.text-effect {
    text-overflow: ellipsis;  /* ... shown when text overflows */
    white-space: nowrap;  /* Prevents text wrapping */
    overflow: hidden;  /* Hides overflow */
    word-wrap: break-word;  /* Wraps long words */
    word-break: break-all;  /* Breaks mid-word if needed */
}
```

**Code Explanation**:
- `overflow: hidden` + `text-overflow: ellipsis` + `white-space: nowrap`: 
  - Creates effect where long text becomes "Text here..."
  - Useful for single-line fields, table cells
- `word-wrap: break-word`: Prevents horizontal scrolling (modern CSS: `overflow-wrap: break-word`)
- `word-break: break-all`: Breaks long words forcefully (useful for URLs)

---

**Positioning**:
```css
.static { position: static; } /* Default - normal flow */

.relative { 
    position: relative;  /* Positioned relative to normal position */
    top: 10px;  /* Moves 10px down from normal position */
    left: 5px;  /* Moves 5px right from normal position */
}

.absolute {
    position: absolute;  /* Positioned relative to nearest positioned parent */
    top: 50px;  /* 50px from top of parent */
    left: 100px;  /* 100px from left of parent */
}

.fixed {
    position: fixed;  /* Positioned relative to viewport (stays on screen) */
    top: 0;  /* At top of viewport */
    right: 0;  /* At right edge */
}

.sticky {
    position: sticky;  /* Toggles between relative and fixed */
    top: 10px;  /* When scrolling, sticks 10px from top */
}

.z-index { z-index: 10; }  /* Controls layering (higher = on top) */
```

**How Positioning Works**:
- `static`: Default (follows normal document flow, top/left/right/bottom ignored)
- `relative`: Moved from its normal position but still takes up space
- `absolute`: Removed from flow, positioned relative to parent (parent must have position set)
- `fixed`: Removed from flow, stays in same place on viewport while scrolling (header/footer effect)
- `sticky`: Hybrid - follows normal flow until scrolling makes it touch specified edge, then sticks

---

**Display and Flexbox**:
```css
.container {
    display: flex;  /* Enables flexbox layout */
    flex-direction: row; /* row, column, row-reverse, column-reverse */
    justify-content: space-between; /* flex-start, center, flex-end, space-around, space-evenly */
    align-items: center; /* flex-start, center, flex-end, stretch */
    gap: 15px;  /* Space between flex items */
}

.item {
    flex: 1; /* Shorthand: flex-grow, flex-shrink, flex-basis */
    flex-grow: 1;  /* Takes equal share of extra space */
    flex-shrink: 1;  /* Shrinks if space limited */
    flex-basis: 200px;  /* Base size before growing/shrinking */
}
```

**How Flexbox Works**:
- `display: flex`: Enables flexbox (container becomes flex container)
- `flex-direction: row`: Items arrange horizontally (column = vertical)
- `justify-content`: Controls spacing along main axis (horizontal if row)
  - `space-between`: Items at edges, space between
  - `center`: Items centered
  - `space-around`: Space around each item
- `align-items`: Controls alignment perpendicular to main axis (vertical if row)
  - `center`: Vertically centered
  - `stretch`: Items fill height
- `gap: 15px`: Space between items
- `flex: 1`: Each item takes equal space (grows/shrinks equally)
- `flex-grow`: How much to grow when space available (3 = 3× more than 1)
- `flex-shrink`: How much to shrink when space limited
- `flex-basis`: Starting size before flex calculations

---

**CSS Grid**:
```css
.grid-container {
    display: grid;  /* Enables grid layout */
    grid-template-columns: 1fr 2fr 1fr;  /* 3 columns: 1/4, 2/4, 1/4 width */
    grid-template-rows: auto 200px auto;  /* 3 rows: auto, fixed, auto height */
    gap: 10px;  /* Space between grid items */
}

.grid-item {
    grid-column: 1 / 3; /* Spans from column 1 to 3 (2 columns wide) */
    grid-row: 1 / 2;  /* Stays in row 1 */
}
```

**How Grid Works**:
- `display: grid`: Enables grid layout
- `grid-template-columns: 1fr 2fr 1fr`:
  - `fr` = fraction unit (proportional)
  - Creates 3 columns where middle is 2× width of other two
- `grid-template-rows`: Defines row heights
  - `auto` = height based on content
  - `200px` = fixed height
- `gap: 10px`: Space between all grid items
- `grid-column: 1 / 3`: Item starts at column 1 and ends before column 3 (spans 2 columns)
- Grid automatically places remaining items in next available space

---

**Lists Styling**:
```css
ul {
    list-style-type: disc; /* disc, circle, square, none */
    list-style-position: inside;  /* inside, outside */
    list-style-image: url('bullet.png');  /* Custom bullet image */
}

ol {
    list-style-type: decimal; /* 1,2,3 */
    /* Other types: lower-alpha, upper-roman, lower-roman */
}

li {
    margin-bottom: 5px;  /* Space below each item */
    padding-left: 10px;  /* Space inside item for text */
}
```

**Code Explanation**:
- `list-style-type: disc`: Changes bullet style
- `list-style-position: outside`: Bullet outside text (default)
- `list-style-image`: Uses custom image as bullet instead of default
- Can style individual `<li>` items

---

**Tables Styling**:
```css
table {
    border-collapse: collapse;  /* Removes space between borders */
    width: 100%;  /* Takes full container width */
}

th, td {
    border: 1px solid #ddd;  /* Border around each cell */
    padding: 12px;  /* Space inside cells */
    text-align: left;  /* Text alignment */
}

th {
    background-color: #4CAF50;  /* Header background color */
    color: white;  /* Header text color */
}

tr:nth-child(even) {
    background-color: #f9f9f9;  /* Alternating row colors */
}

tr:hover {
    background-color: #f5f5f5;  /* Highlight row on hover */
}
```

**Code Explanation**:
- `border-collapse: collapse`: Adjacent borders merge into single border
- `th, td`: Styles both header and data cells
- `th`: Header styling (background color, white text)
- `tr:nth-child(even)`: Zebra striping (alternate rows light colored)
- `tr:hover`: When mouse hovers over row, background changes (better readability)

---

**Menu Design**:
```css
nav ul {
    list-style: none;  /* Removes bullets */
    display: flex;  /* Horizontal menu */
    background-color: #333;  /* Dark background */
}

nav li {
    flex: 1;  /* Equal width menu items */
}

nav a {
    display: block;  /* Makes link fill entire item space */
    padding: 15px 20px;  /* Internal space */
    color: white;  /* Link color */
    text-decoration: none;  /* Removes underline */
    text-align: center;  /* Centers text */
}

nav a:hover {
    background-color: #555;  /* Lighter background on hover */
    color: #fff;  /* Text color on hover */
}

nav a.active {
    background-color: #4CAF50;  /* Current page color */
}
```

**How Menu Works**:
- `display: flex`: Items arranged horizontally
- `flex: 1`: Each item takes equal space
- `display: block` on link: Makes entire item clickable (not just text)
- `:hover`: Changes appearance when user hovers
- `.active` class: Applied to current page link via JavaScript/PHP

---

**Transitions and Transforms**:
```css
.box {
    transition: all 0.3s ease-in-out;  /* Smooth animation on changes */
    transform: translateX(10px);  /* Move 10px right */
    transform: rotate(45deg);  /* Rotate 45 degrees */
    transform: scale(1.5);  /* Make 1.5× larger */
    transform: skew(20deg);  /* Slant text 20 degrees */
}

.box:hover {
    transform: translateX(50px) rotate(10deg);  /* Multiple transforms at once */
}
```

**Code Explanation**:
- `transition: all 0.3s ease-in-out`:
  - `all`: Animate all property changes
  - `0.3s`: Duration of animation
  - `ease-in-out`: Animation acceleration (starts slow, speeds up, slows down)
- `transform: translateX(10px)`: Move element (X=horizontal, Y=vertical)
- `transform: rotate(45deg)`: Rotate element by angle
- `transform: scale(1.5)`: Grow/shrink (1.5 = 150% size)
- `transform: skew()`: Slant/shear element
- Multiple transforms can be combined in one property

---

**Animations**:
```css
@keyframes slide {
    0% { transform: translateX(0); }  /* Starting position */
    50% { transform: translateX(100px); }  /* Middle point */
    100% { transform: translateX(200px); }  /* End position */
}

.animated-box {
    animation: slide 2s infinite;  /* Run 'slide' animation for 2 seconds, repeat */
}
```

**Code Explanation**:
- `@keyframes slide`: Defines animation named "slide"
- `0%, 50%, 100%`: Key frames at these percentages of animation duration
- `transform` properties change at each keyframe (browser interpolates between)
- `animation: slide 2s infinite`:
  - `slide`: Use this animation
  - `2s`: Duration
  - `infinite`: Repeat forever
- Other options: `animation-delay`, `animation-direction`, `animation-timing-function`

---

**Responsive Design Principles**:
```css
/* Mobile First Approach - Start with mobile styles */
.container {
    font-size: 14px;
    width: 100%;
}

/* Tablet - Screen width 768px or larger */
@media (min-width: 768px) {
    .container {
        font-size: 16px;
        width: 90%;
    }
}

/* Desktop - Screen width 1024px or larger */
@media (min-width: 1024px) {
    .container {
        font-size: 18px;
        width: 80%;
        max-width: 1200px;
    }
}
```

**How Responsive Design Works**:
- `@media (min-width: 768px)`: Media query (CSS applies only if condition true)
- `min-width: 768px`: Condition applies to screens 768px or wider
- "Mobile first" approach: Default styles for mobile, override with larger screen styles
- Allows single HTML file to look good on all screen sizes
- Common breakpoints: 768px (tablet), 1024px (desktop), 1440px (large desktop)

---

### **Bootstrap - Mobile Responsive Website**

**Introduction**: Bootstrap is a CSS framework providing pre-built responsive components, grid system, and utilities, saving development time.

**Basic Grid System**:
```html
<!DOCTYPE html>
<html>
<head>
    <!-- Bootstrap CSS from CDN (Content Delivery Network) -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
<body>
    <div class="container-fluid">  <!-- Full-width container -->
        <div class="row">  <!-- Row for columns -->
            <div class="col-md-6">Column 1 (50% on medium+ screens)</div>
            <div class="col-md-6">Column 2 (50% on medium+ screens)</div>
        </div>
    </div>
    
    <!-- Bootstrap JavaScript for interactive components -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
```

**How Bootstrap Grid Works**:
- `container-fluid`: Full-width container (stretches to screen edge)
  - Alternative: `container` for fixed max-width
- `row`: Wrapper for columns (creates horizontal layout)
- `col-md-6`: Column spanning 6 out of 12 Bootstrap columns on medium screens and up
  - 12-column grid system
  - `col-md-6` = 50% width on medium+ screens
  - On smaller screens (mobile), columns stack 100% width

**Bootstrap Components**:
- **Navbar**: Navigation bar (`<nav class="navbar">`)
- **Cards**: Content containers (`<div class="card">`)
- **Buttons**: Pre-styled buttons (`.btn .btn-primary`)
- **Forms**: Form styling (`.form-control` on inputs)
- **Modal**: Dialog boxes (popup windows)
- **Carousel**: Image sliders
- **Alerts**: Notification boxes
- **Badges**: Small count labels
- **Breadcrumbs**: Navigation path
- **Pagination**: Page navigation

**Responsive Classes**:
- `col-xs-*` (extra small), `col-sm-*` (small), `col-md-*` (medium)
- `col-lg-*` (large), `col-xl-*` (extra large), `col-xxl-*` (2x extra large)
- `d-none` (hide), `d-md-block` (show on medium+ screens)

**Bootstrap Utilities**:
- **Margin/Padding**: `m-1` (margin), `mt-2` (margin-top), `mb-3` (margin-bottom)
  - Suffixes: `x` (left+right), `y` (top+bottom), `auto` (center)
  - Scale: 1-5 (increases in increments)
- **Text**: `text-center`, `text-start`, `text-end`, `text-bold`
- **Display**: `d-flex`, `justify-content-center`, `align-items-center`

---

## UNIT II: JavaScript

### **JavaScript Fundamentals**

#### **Variables**
```javascript
// var - function scoped (avoid in modern JavaScript)
var x = 10;

// let - block scoped (preferred for variables that change)
let name = "John";

// const - block scoped, cannot be reassigned (preferred for constants)
const PI = 3.14159;

const person = { name: "John" };
person.age = 25; // Allowed - modifying object properties
// person = {}; // Error - cannot reassign const variable
```

**How It Works**:
- Variables store data values
- `var`: Old way (scope issues, avoid)
- `let`: Modern way (block scope = limited to { })
- `const`: For values that shouldn't change (actually means reference can't change, properties can)
- Declaring variable name makes it available for use
- Variable names are case-sensitive (name ≠ Name)

---

#### **Data Types**
```javascript
// Primitives (simple values)
let num = 42;              // Number - integers and decimals
let str = "Hello";         // String - text
let bool = true;           // Boolean - true/false
let undef = undefined;     // Undefined - no value assigned
let nul = null;            // Null - intentional empty value
let sym = Symbol('id');    // Symbol - unique identifier

// Non-primitives (complex values, objects)
let arr = [1, 2, 3];       // Array - ordered list
let obj = { key: 'value' }; // Object - key-value pairs
```

**Code Explanation**:
- **Number**: Any numeric value (42, 3.14, -5, Infinity)
- **String**: Text in quotes ("hello" or 'hello')
- **Boolean**: Only true or false (used in conditions)
- **undefined**: Variable declared but no value assigned
- **null**: Intentionally set to no value (different from undefined)
- **Symbol**: Unique, used rarely (mostly internal use)
- **Array**: List of values accessed by index (0, 1, 2...)
- **Object**: Key-value pairs (property: value)

---

#### **Operators**
```javascript
// Arithmetic Operators - Mathematical operations
let sum = 10 + 5;      // 15 (addition)
let diff = 10 - 5;     // 5 (subtraction)
let prod = 10 * 5;     // 50 (multiplication)
let div = 10 / 5;      // 2 (division)
let mod = 10 % 3;      // 1 (remainder/modulo)
let exp = 2 ** 3;      // 8 (exponentiation, 2^3)

// Assignment Operators - Assign/modify variables
let x = 5;
x += 3;  // x = 8 (add then assign)
x -= 2;  // x = 6 (subtract then assign)
x *= 2;  // x = 12 (multiply then assign)
x /= 3;  // x = 4 (divide then assign)

// Comparison Operators - Compare values (return true/false)
5 == '5';   // true (loose equality, ignores type)
5 === '5';  // false (strict equality, checks type)
5 != '5';   // false (not equal loose)
5 !== '5';  // true (not equal strict)
5 < 10;     // true (less than)
5 > 3;      // true (greater than)
5 <= 5;     // true (less than or equal)
5 >= 5;     // true (greater than or equal)

// Logical Operators - Combine conditions
true && false;  // false (AND - both must be true)
true || false;  // true (OR - at least one true)
!true;          // false (NOT - reverse boolean)

// Ternary Operator - Conditional assignment (shorthand if-else)
let age = 20;
let status = age >= 18 ? "Adult" : "Minor";  // status = "Adult"
```

**Code Explanation**:
- **Arithmetic**: Do math operations
- **Assignment**: Store/modify values
- **Comparison**: Check if values match conditions
  - `==` vs `===`: Use strict (`===`) to avoid type confusion (5 == '5' is true, 5 === '5' is false)
- **Logical**: Combine multiple conditions
  - `&&` (AND): Both conditions must be true
  - `||` (OR): At least one condition true
  - `!` (NOT): Reverses true/false
- **Ternary**: Like if-else in one line (condition ? ifTrue : ifFalse)

---

#### **Control Structures**
```javascript
// if-else - Execute code based on condition
if (age < 18) {
    console.log("Minor");
} else if (age < 65) {
    console.log("Adult");
} else {
    console.log("Senior");
}

// switch - Multiple conditions (cleaner than many if-else)
switch (day) {
    case 1:
        console.log("Monday");
        break;  // Exit switch after executing case
    case 2:
        console.log("Tuesday");
        break;
    default:
        console.log("Other day");  // Runs if no case matches
}
```

**Code Explanation**:
- `if (condition)`: Execute block if true
- `else if`: Check another condition if first false
- `else`: Execute if all previous conditions false
- `switch`: Cleaner way to check single variable against many values
- `case value:`: If variable equals this value, execute following code
- `break`: Exits switch (without it, code "falls through" to next case)
- `default`: Like else (runs if no case matches)

---

#### **Looping Constructs**
```javascript
// for loop - Run code fixed number of times
for (let i = 0; i < 5; i++) {  // Start at 0, loop while < 5, increment i
    console.log(i);  // Prints: 0, 1, 2, 3, 4
}

// while loop - Run while condition true
let count = 0;
while (count < 5) {  // Loop continues as long as true
    console.log(count);
    count++;
}

// do-while loop - Run at least once, then check condition
let num = 0;
do {
    console.log(num);
    num++;
} while (num < 5);  // Checked after execution

// for...in loop - Iterate over object keys
const obj = { a: 1, b: 2, c: 3 };
for (let key in obj) {
    console.log(key, obj[key]);  // Prints: a 1, b 2, c 3
}

// for...of loop - Iterate over array values
const arr = [10, 20, 30];
for (let value of arr) {
    console.log(value);  // Prints: 10, 20, 30
}

// forEach - Built-in array method (cleaner for arrays)
arr.forEach((item, index) => {
    console.log(index, item);  // Prints: 0 10, 1 20, 2 30
});
```

**Code Explanation**:
- **for**: Traditional loop with counter
  - `let i = 0`: Initialize variable
  - `i < 5`: Continue while true
  - `i++`: Run after each iteration
- **while**: Loop while condition true (check before execution)
- **do-while**: Loop while condition true (check after execution, runs at least once)
- **for...in**: Loops over object keys (property names)
- **for...of**: Loops over array values (modern, cleaner)
- **forEach**: Array method that runs function for each element

---

#### **Break and Continue**
```javascript
// Break - Exit loop immediately
for (let i = 0; i < 10; i++) {
    if (i === 5) break;  // Exit loop when i reaches 5
    console.log(i);  // Prints: 0, 1, 2, 3, 4
}

// Continue - Skip rest of iteration, go to next
for (let i = 0; i < 5; i++) {
    if (i === 2) continue;  // Skip when i is 2
    console.log(i);  // Prints: 0, 1, 3, 4 (skips 2)
}
```

**Code Explanation**:
- `break`: Immediately exits loop (stops iteration)
- `continue`: Skips current iteration and goes to next

---

#### **Functions**
```javascript
// Function Declaration - Reusable block of code
function add(a, b) {  // Parameters: a, b
    return a + b;  // Return result
}
console.log(add(5, 3));  // Call function, prints: 8

// Function Expression - Function stored in variable
const multiply = function(a, b) {
    return a * b;
};
console.log(multiply(4, 5));  // Prints: 20

// Arrow Function (ES6) - Modern compact syntax
const divide = (a, b) => a / b;  // Short version
const greet = (name) => {  // Full version with multiple statements
    let greeting = `Hello, ${name}`;
    console.log(greeting);
};

// Default Parameters - Value if parameter not provided
function greetUser(name = "Guest") {
    console.log(`Welcome, ${name}`);
}
greetUser();  // Prints: Welcome, Guest

// Rest Parameters - Accept any number of arguments
function sum(...numbers) {
    return numbers.reduce((a, b) => a + b, 0);  // Add all numbers
}
console.log(sum(1, 2, 3, 4));  // Prints: 10
```

**How Functions Work - General Overview**:
Functions package code into reusable blocks. You define parameters (inputs), code runs when called, returns result.

**Component Breakdown**:
- `function` keyword: Declares function
- `(a, b)`: Parameters (variable names for inputs)
- `add(5, 3)`: Calling function with arguments (actual values)
- `return`: Sends result back to caller
- `const multiply = function() {}`: Store function in variable
- Arrow function `=>`: Modern syntax (more concise)
- `...numbers`: Rest operator (collects all arguments into array)

---

#### **Recursion**
```javascript
// Factorial - Example recursive function
function factorial(n) {
    if (n <= 1) return 1;  // Base case: stop recursion
    return n * factorial(n - 1);  // Recursive call
}
console.log(factorial(5));  // Prints: 120 (5*4*3*2*1)

// Fibonacci - Another recursive example
function fibonacci(n) {
    if (n <= 1) return n;  // Base cases
    return fibonacci(n - 1) + fibonacci(n - 2);  // Recursive call
}
console.log(fibonacci(6));  // Prints: 8
```

**Code Explanation**:
- Recursion: Function calling itself with simpler input
- Base case: Condition to stop recursion (prevents infinite loop)
- Recursive case: Function calls itself with simpler problem
- Each call adds to call stack; when base case reached, stack unwinds

---

#### **Arrays**
```javascript
// Declaration
let arr1 = [1, 2, 3];  // Array literal
let arr2 = new Array(10);  // Empty array with 10 slots

// Common Methods
arr.push(4);           // Add to end: [1, 2, 3, 4]
arr.pop();             // Remove from end, returns removed item
arr.unshift(0);        // Add to beginning: [0, 1, 2, 3]
arr.shift();           // Remove from beginning
arr.length;            // Get number of items
arr.reverse();         // Reverse order
arr.sort();            // Sort items

// Higher-order Functions (take function as argument)
arr.map(x => x * 2);   // Transform each: [2, 4, 6, 8]
arr.filter(x => x > 2); // Keep only matches: [3, 4]
arr.reduce((acc, x) => acc + x, 0); // Combine to single: 10
arr.find(x => x > 5);  // First matching item: 6
arr.some(x => x > 5);  // At least one matches: true
arr.every(x => x > 0); // All match condition: true
arr.includes(5);       // Contains item: true
```

**Code Explanation**:
- **Mutating methods** (change original):
  - `push`, `pop`, `shift`, `unshift`: Add/remove items
  - `reverse`, `sort`: Change order
- **Non-mutating methods** (return new array/value):
  - `map`: Transform each item (returns new array)
  - `filter`: Keep matching items (returns new array)
  - `reduce`: Combine items into single value
  - `find`: Return first match
  - `some`/`every`: Check if any/all match condition
  - `includes`: Check if contains item

---

#### **Passing Arrays to Functions**
```javascript
// Arrays are passed by reference (changes affect original)
function modifyArray(arr) {
    arr[0] = 999;  // Modifies original array
}

let myArray = [1, 2, 3];
modifyArray(myArray);
console.log(myArray);  // [999, 2, 3] - Original changed!

// To avoid modification, create copy using spread operator
const copyArray = [...myArray];  // [...] creates new array
modifyArray(copyArray);
console.log(myArray);  // [1, 2, 3] - Original unchanged
```

**Code Explanation**:
- Arrays are reference types (variable holds address, not value)
- Passing array to function passes the reference (both point to same array)
- Modifying in function affects original
- `[...array]`: Spread operator unpacks array and creates new copy
- Now function modifies copy, not original

---

#### **Form Validation in JavaScript**
```html
<form id="myForm" onsubmit="validateForm(event)">
    <input type="text" id="username" placeholder="Username">
    <input type="email" id="email" placeholder="Email">
    <input type="password" id="password" placeholder="Password" minlength="6">
    <button type="submit">Submit</button>
</form>

<script>
function validateForm(event) {
    event.preventDefault();  // Prevent default form submission
    
    // Get input values
    const username = document.getElementById('username').value.trim();
    const email = document.getElementById('email').value.trim();
    const password = document.getElementById('password').value;
    
    // Validate username
    if (username === '') {
        alert('Username is required');
        return false;
    }
    
    // Validate email (regex pattern for email format)
    const emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    if (!emailPattern.test(email)) {
        alert('Invalid email format');
        return false;
    }
    
    // Validate password
    if (password.length < 6) {
        alert('Password must be at least 6 characters');
        return false;
    }
    
    // All valid
    alert('Form submitted successfully!');
    // document.getElementById('myForm').submit();  // Actually submit
}
</script>
```

**How It Works - General Overview**:
Validation checks user input before sending to server. Catches errors early, improves UX, provides feedback.

**Component Breakdown**:
- `onsubmit="validateForm(event)"`: Calls function when submit clicked
- `event.preventDefault()`: Stops default form submission (lets us validate first)
- `getElementById()`: Gets input element
- `.value`: Gets text user entered
- `.trim()`: Removes spaces before/after
- `=== ''`: Checks if empty
- Email regex pattern: `/^[^\s@]+@[^\s@]+\.[^\s@]+$/`
  - `^` = start of string
  - `[^\s@]+` = characters except whitespace and @
  - `@` = literal @ symbol
  - `\\.` = literal dot (escaped)
  - `$` = end of string
- `.test()`: Returns true/false if pattern matches
- `return false`: Prevents submission, form stays open
- Show alert to tell user what's wrong

---

### **JavaScript Objects**

#### **Date Object**
```javascript
// Create Date
let now = new Date();  // Current date/time
let specific = new Date(2024, 11, 25);  // Year, Month (0-11), Day

// Get date components
now.getFullYear();        // 2024
now.getMonth();           // 0-11 (November is 10)
now.getDate();            // 1-31 (day of month)
now.getDay();             // 0-6 (Sunday is 0, Saturday is 6)
now.getHours();           // 0-23 (hour of day)
now.getMinutes();         // 0-59
now.getSeconds();         // 0-59
now.getTime();            // Milliseconds since Jan 1, 1970

// Format output
now.toString();           // Full format: "Sat Nov 29 2025..."
now.toDateString();       // Date only: "Sat Nov 29 2025"
now.toISOString();        // ISO format: "2025-11-29T12:30:00.000Z"
```

**Code Explanation**:
- `new Date()`: Creates Date object (constructor)
- `getFullYear()`, `getMonth()`, etc.: Extract date components
- Note: `getMonth()` returns 0-11 (need to add 1 to get human month)
- Methods return different formats for different uses

---

#### **String Object**
```javascript
let str = "JavaScript";

// Properties
str.length;                    // 10 (number of characters)

// Methods
str.charAt(0);                 // "J" (character at index 0)
str.charCodeAt(0);             // 74 (ASCII code of character)
str.toUpperCase();             // "JAVASCRIPT"
str.toLowerCase();             // "javascript"
str.indexOf("S");              // 4 (position of "S", -1 if not found)
str.substring(0, 4);           // "Java" (characters from index 0 to 4)
str.slice(0, 4);               // "Java" (same as substring)
str.split("");                 // ['J','a','v','a',...] (split into array)
str.replace("Java", "Type");   // "TypeScript" (replace first occurrence)
str.trim();                    // Remove spaces before/after
str.startsWith("Java");        // true (starts with this?)
str.endsWith("Script");        // true (ends with this?)
str.includes("Script");        // true (contains this?)
str.repeat(2);                 // "JavaScriptJavaScript" (repeat 2 times)
```

**Code Explanation**:
- `.length`: Number of characters
- `.charAt(index)`: Character at position
- `.toUpperCase()`, `.toLowerCase()`: Case conversion
- `.indexOf()`: Find position (returns -1 if not found)
- `.substring(start, end)`, `.slice()`: Extract portion
- `.split()`: Break string into array at delimiter
- `.replace()`: Replace first match (or use `/pattern/g` for all)
- `.trim()`: Remove whitespace ends
- `.startsWith()`, `.endsWith()`: Check beginning/end
- `.includes()`: Check if contains
- `.repeat()`: Repeat string multiple times

---

#### **Boolean Object**
```javascript
let bool = new Boolean(true);  // Object wrapper (rarely used)
let primitive = true;          // Primitive (normal way)

// Truthiness - values converting to true/false
Boolean(1);        // true (any non-zero number)
Boolean(0);        // false
Boolean("");       // false (empty string)
Boolean("text");   // true (non-empty string)
Boolean(null);     // false
Boolean(undefined); // false
Boolean(NaN);      // false (Not a Number)
Boolean([]);       // true (arrays are truthy)
Boolean({});       // true (objects are truthy)
```

**Code Explanation**:
- Boolean values are true or false
- JavaScript converts values to boolean in conditions
- Falsy values: false, 0, "", null, undefined, NaN
- Truthy values: everything else
- Use `Boolean()` to explicitly convert

---

#### **Window Object**
```javascript
// Global object in browsers (represents browser window)
window.console.log("Hello");  // Can access from window
window.alert("Alert message");  // Show popup
window.confirm("Continue?");  // Yes/No dialog
window.prompt("Enter name:");  // Input dialog

// Properties (information about window)
window.innerWidth;      // Width of viewport (content area)
window.innerHeight;     // Height of viewport
window.location;        // Current URL and location object
window.history;         // Browser history (back, forward)
window.navigator;       // Browser and OS information

// Methods (actions on window)
window.open("url");     // Open new window
window.close();         // Close window (only works on window you opened)
window.setTimeout(() => {}, 1000);   // Run code after delay
window.setInterval(() => {}, 1000);  // Run code repeatedly
```

**Code Explanation**:
- `window`: Global object (everything in browser is part of window)
- `alert()`, `confirm()`, `prompt()`: User interaction dialogs
- `location`: Object containing URL, hostname, path
- `history`: Can navigate back/forward
- `setTimeout()`: Schedule code to run once after delay (in milliseconds)
- `setInterval()`: Schedule code to run repeatedly at interval

---

#### **Document Object**
```javascript
// Access elements
document.getElementById("id");           // By ID (unique)
document.querySelector(".class");        // By CSS selector (first match)
document.querySelectorAll("p");          // All p elements
document.getElementsByTagName("div");    // All div elements (HTMLCollection)

// Properties (document info)
document.title;                          // Page title (from <title>)
document.URL;                            // Current page URL
document.domain;                         // Domain name
document.body;                           // <body> element
document.head;                           // <head> element

// Methods (modify document)
document.createElement("div");           // Create new element
document.write("Text");                  // Write to document (careful!)
```

**Code Explanation**:
- `document`: Represents entire HTML page
- `getElementById()`: Most efficient (IDs are unique)
- `querySelector()`: Flexible (uses CSS selectors)
- `querySelectorAll()`: Get multiple elements (returns NodeList)
- `getElementById()` returns single element or null
- `getElementsByTagName()` returns live HTMLCollection
- `createElement()`: Make new element (not yet in page, must append)
- `document.write()`: Overwrites page if after load (avoid in production)

---

#### **Cookies**
```javascript
// Set cookie (persists on client machine)
document.cookie = "username=John; expires=Thu, 31-Dec-2025 23:59:59 UTC; path=/";
// Format: name=value; expires=date; path=path

// Get cookies (all cookies as string)
console.log(document.cookie);
// Output: "username=John; theme=dark"

// Delete cookie (set expiration to past date)
document.cookie = "username=; expires=Thu, 01 Jan 1970 00:00:00 UTC; path=/;";

// Helper function to get specific cookie value
function getCookie(name) {
    let nameEQ = name + "=";
    let cookies = document.cookie.split(';');  // Split into array
    for (let i = 0; i < cookies.length; i++) {
        let cookie = cookies[i].trim();  // Remove spaces
        if (cookie.indexOf(nameEQ) === 0) {  // If starts with name=
            return cookie.substring(nameEQ.length);  // Return value
        }
    }
    return null;  // Not found
}

// Usage
getCookie("username");  // Returns "John"
```

**Code Explanation**:
- Cookies: Small data files stored on client (persists across sessions)
- `document.cookie`: Set new cookie or append to existing
- Format: `name=value; expires=date; path=/; domain=.example.com`
- `expires`: When cookie expires (deleted automatically after)
- `path=/`: Cookie available everywhere on site
- Cookie string contains all cookies: "name1=value1; name2=value2"
- Must parse manually to get specific cookie
- `split(';')`: Break cookie string into array
- `trim()`: Remove whitespace
- `indexOf()`: Check if cookie starts with name

---

#### **Document Object Model (DOM)**
```javascript
// Selecting elements
const element = document.getElementById("myId");
const elements = document.querySelectorAll(".myClass");

// Modifying elements
element.textContent = "New text";  // Change text (plain text only)
element.innerHTML = "<strong>Bold text</strong>";  // Change content (HTML allowed)
element.style.color = "red";  // Change inline CSS
element.style.fontSize = "20px";

// Managing classes
element.classList.add("active");     // Add class
element.classList.remove("active");  // Remove class
element.classList.toggle("active");  // Add if not present, remove if present

// Managing attributes
element.setAttribute("id", "newId");  // Set attribute value
element.getAttribute("id");           // Get attribute value
element.removeAttribute("id");        // Remove attribute

// Navigating DOM tree
element.parentElement;      // Parent element
element.children;           // All child elements (HTMLCollection)
element.firstChild;         // First child (including text nodes)
element.firstElementChild;  // First child element
element.nextSibling;        // Next sibling (including text nodes)
element.nextElementSibling; // Next sibling element
```

**How DOM Works - General Overview**:
DOM represents HTML as tree structure. JavaScript can navigate, read, modify elements.

**Component Breakdown**:
- `textContent`: Plain text (safe, ignores HTML tags)
- `innerHTML`: HTML content (can include tags, use carefully with user input)
- `style.property = "value"`: Inline CSS styling
- `classList.add()`: Add CSS class (preferred over string manipulation)
- `classList.toggle()`: Add if absent, remove if present
- `parentElement`: Direct parent in tree
- `children`: Only element children (not text)
- `firstChild` vs `firstElementChild`: First includes text nodes, second doesn't

---

#### **Event Handling**
```html
<!-- HTML -->
<button id="myBtn">Click Me</button>
<input type="text" id="myInput">

<script>
// Method 1: addEventListener (Recommended)
const btn = document.getElementById('myBtn');
btn.addEventListener('click', function(event) {
    console.log('Button clicked');
    console.log(event.target);  // Element that triggered event
});

// Method 2: Inline attribute (onchange)
btn.onclick = function() {
    console.log('Button clicked');
};

// Page lifecycle events
document.addEventListener('DOMContentLoaded', function() {
    console.log('DOM fully loaded - safe to access elements');
    // Run code here when page ready
});

// Input change events
const input = document.getElementById('myInput');
input.addEventListener('change', function() {
    console.log('Input changed: ' + this.value);  // Fires when user finishes editing
});

input.addEventListener('input', function() {
    console.log('User typing: ' + this.value);  // Fires while typing
});

// Focus events
input.addEventListener('focus', function() {
    console.log('Input focused');  // User clicked in field
});

input.addEventListener('blur', function() {
    console.log('Input lost focus');  // User left field
});

// Window events
window.addEventListener('resize', function() {
    console.log('Window resized');
    console.log('Width: ' + window.innerWidth);
});

// Keyboard events
document.addEventListener('keypress', function(event) {
    console.log('Key pressed: ' + event.key);  // Which key
});

// Scroll events
document.addEventListener('scroll', function() {
    console.log('Page scrolled');
    console.log('Scroll position: ' + window.scrollY);
});
</script>
```

**How Event Handling Works - General Overview**:
Events are user actions (click, type, scroll). Browser detects events and runs code you attach.

**Component Breakdown**:
- `addEventListener()`: Register function to run when event occurs
- `event`: Object containing event information
- `event.target`: Element that triggered event
- `event.key`: Which key pressed (for keyboard events)
- `this`: Refers to element event occurred on
- `DOMContentLoaded`: Fires after HTML parsed (before all images loaded)
- `change`: Fires when input loses focus and value changed
- `input`: Fires while typing (real-time)
- `focus`/`blur`: When input gains/loses focus
- `resize`: When window resized
- `keypress`/`keydown`/`keyup`: Keyboard events
- `scroll`: When page scrolled

**Common Event Types**:
- **Mouse**: `click`, `dblclick`, `mouseover`, `mouseout`, `mousedown`, `mouseup`, `mousemove`
- **Keyboard**: `keydown`, `keyup`, `keypress`
- **Form**: `submit`, `change`, `input`, `focus`, `blur`, `reset`
- **Window**: `load`, `unload`, `resize`, `scroll`
- **Touch**: `touchstart`, `touchend`, `touchmove`

---

## UNIT III: PHP and MySQL

### **PHP Introduction**

#### **Installation and Configuration**
- Download from **php.net**
- Install XAMPP/WAMP/LAMP stack (bundles PHP, MySQL, Apache)
- Configure `php.ini` file (server settings)
- Restart Apache server
- Test: Create `info.php` with `<?php phpinfo(); ?>` and view in browser

---

#### **Variables and Data Types**
```php
<?php
// Variables - Store data in memory
$name = "John";           // String - text
$age = 25;                // Integer - whole number
$salary = 50000.50;       // Float - decimal number
$isActive = true;         // Boolean - true/false

// Data Types
$integer = 100;           // Numbers without decimal
$float = 3.14;            // Numbers with decimal point
$string = "Hello";        // Text in quotes
$boolean = false;         // true or false only
$array = array(1, 2, 3);  // List of values
$object = new stdClass(); // Object instance
$null_var = NULL;         // Intentional empty

// Type Checking (determine what type variable is)
is_int($age);             // true if integer
is_string($name);         // true if string
is_array($array);         // true if array
is_bool($isActive);       // true if boolean
is_null($null_var);       // true if NULL
gettype($age);            // Returns type as string: "integer"

// Type Casting (convert to different type)
(int)"123";               // Convert string to integer: 123
(string)123;              // Convert to string: "123"
(float)"3.14";            // Convert to float: 3.14
(bool)1;                  // Convert to boolean: true
?>
```

**Code Explanation**:
- Variables start with `$` (PHP requirement)
- Variable names case-sensitive (`$name` ≠ `$Name`)
- `=` assigns value
- Type checking functions verify what type data is
- Type casting in parentheses converts between types

---

#### **Operators**
```php
<?php
// Arithmetic Operators - Math operations
$sum = 10 + 5;    // 15 (addition)
$diff = 10 - 5;   // 5 (subtraction)
$prod = 10 * 5;   // 50 (multiplication)
$div = 10 / 5;    // 2 (division)
$mod = 10 % 3;    // 1 (remainder)

// String Operator - Concatenate strings
$str1 = "Hello";
$str2 = " World";
$result = $str1 . $str2;  // "Hello World" (dot concatenates)

// Assignment Operators - Assign/modify values
$x = 5;
$x += 3;           // $x = 8 (add then assign)
$x -= 2;           // $x = 6 (subtract then assign)
$x *= 2;           // $x = 12 (multiply then assign)
$x /= 3;           // $x = 4 (divide then assign)
$x .= " text";     // $x = "4 text" (concatenate then assign)

// Comparison Operators - Compare values (true/false)
5 == "5";          // true (loose equality, ignores type)
5 === "5";         // false (strict equality, checks type)
5 != 3;            // true (not equal)
5 !== "5";         // true (not equal strict)
5 < 10;            // true (less than)
5 > 3;             // true (greater than)
5 <= 5;            // true (less than or equal)
5 >= 5;            // true (greater than or equal)

// Logical Operators - Combine conditions
true && false;     // false (AND - both must be true)
true || false;     // true (OR - at least one true)
!true;             // false (NOT - reverse)
?>
```

**Code Explanation**:
- Similar to JavaScript
- `.` is string concatenation (not `+`)
- Use `===` for strict comparison (safer)

---

#### **Constants**
```php
<?php
// Define constant (cannot be changed later)
define("SITE_NAME", "My Website");              // Always available
define("SITE_URL", "https://example.com", true); // Case-insensitive

// Use constants (no $ symbol)
echo SITE_NAME;  // Prints: My Website

// Class constants (belong to class)
class MyClass {
    const VERSION = "1.0";  // Cannot be changed
}
echo MyClass::VERSION;  // Prints: 1.0

// Difference from variables:
// Constants: Cannot be changed, no $, defined once
// Variables: Can be changed, require $, defined with =
?>
```

**Code Explanation**:
- Constants defined with `define()` or `const`
- No `$` when using constants
- Cannot be undefined or redefined
- Used for values that never change (config, system info)

---

#### **Arrays**
```php
<?php
// Indexed Array - Access by position (0, 1, 2...)
$colors = array("Red", "Green", "Blue");
$colors = ["Red", "Green", "Blue"];  // Short syntax (PHP 5.4+)
echo $colors[0];  // "Red" (first item)

// Associative Array - Access by key (like JavaScript objects)
$person = array(
    "name" => "John",   // => means "maps to"
    "age" => 25,
    "city" => "New York"
);
$person = [
    "name" => "John",
    "age" => 25,
    "city" => "New York"
];
echo $person["name"];  // "John"

// Multidimensional Array - Array of arrays
$students = array(
    array("John", 25, "Science"),
    array("Jane", 24, "Commerce"),
    array("Bob", 26, "Arts")
);
echo $students[0][0];  // "John" (first row, first column)

// Array Functions
count($colors);              // 3 (number of items)
in_array("Red", $colors);    // true (is Red in array?)
array_push($colors, "Yellow");  // Add to end
array_pop($colors);          // Remove from end
array_merge($colors, ["Pink"]); // Combine arrays
sort($colors);               // Sort ascending
rsort($colors);              // Sort descending
?>
```

**Code Explanation**:
- Indexed array: Position-based access (0-based like JavaScript)
- Associative array: Key-value pairs (like JavaScript objects)
- `=>` maps key to value
- Multidimensional: Nested arrays
- `[row][column]` access nested items
- Array functions perform common operations

---

#### **Looping with Arrays**
```php
<?php
$items = ["Apple", "Banana", "Cherry"];

// foreach loop - Most common, works with any array
foreach ($items as $item) {
    echo $item . "<br>";  // Apple, Banana, Cherry
}

// foreach with key-value (associative array)
$person = ["name" => "John", "age" => 25, "city" => "NYC"];
foreach ($person as $key => $value) {
    echo "$key: $value<br>";  // name: John, age: 25, city: NYC
}

// for loop - Traditional (more control)
for ($i = 0; $i < count($items); $i++) {
    echo $items[$i] . "<br>";
}

// while loop
$i = 0;
while ($i < count($items)) {
    echo $items[$i] . "<br>";
    $i++;
}

// Note: each() and while loop (deprecated in PHP 7.2+)
// Use foreach instead (modern, cleaner)
?>
```

**Code Explanation**:
- `foreach`: Iterate through array (value only or key=>value)
- Works with both indexed and associative arrays
- Variable after `as` gets each item
- `$key => $value`: Both key and value in each iteration
- `for` loop: More control, can increment/decrement
- `while` loop: Run while condition true
- `foreach` is preferred (simpler, less error-prone)

---

#### **Objects**
```php
<?php
// Class Definition
class Person {
    // Properties (variables in class)
    public $name;          // Accessible everywhere
    private $age;          // Accessible only in class
    
    // Constructor (runs when object created)
    public function __construct($name, $age) {
        $this->name = $name;  // $this refers to current object
        $this->age = $age;
    }
    
    // Method (function in class)
    public function getAge() {
        return $this->age;  // Access private property
    }
    
    // Setter method
    public function setAge($age) {
        if ($age > 0) {
            $this->age = $age;
        }
    }
}

// Create Object (instance of class)
$person = new Person("John", 25);
echo $person->name;         // "John"
echo $person->getAge();     // 25
$person->setAge(26);        // Change age
echo $person->getAge();     // 26
?>
```

**Code Explanation**:
- Class: Blueprint for objects
- Properties: Variables in class (public/private control access)
- Methods: Functions in class
- `__construct()`: Special method runs when object created (initialization)
- `$this->`: Access properties/methods of current object
- `new`: Create object instance
- `->`: Arrow operator to access object properties/methods

---

#### **String Processing**
```php
<?php
$str = "Hello World";

// String Functions
strlen($str);              // 11 (number of characters)
strtoupper($str);          // "HELLO WORLD"
strtolower($str);          // "hello world"
ucfirst($str);             // "Hello world" (first letter uppercase)
ucwords($str);             // "Hello World" (each word uppercase)
trim($str);                // Remove spaces before/after
strpos($str, "World");     // 6 (position of "World", -1 if not found)
substr($str, 0, 5);        // "Hello" (substring from 0 to 5)
str_replace("World", "PHP", $str);  // "Hello PHP"
explode(" ", $str);        // ["Hello", "World"] (split into array)
implode("-", ["a", "b"]); // "a-b" (join array with delimiter)
str_repeat($str, 2);       // "Hello WorldHello World"

// String comparison
strcmp("hello", "hello");        // 0 (equal)
strcasecmp("Hello", "hello");    // 0 (equal, ignores case)
?>
```

**Code Explanation**:
- String functions manipulate text
- Most return new string (don't modify original)
- `strpos()`: Find first occurrence (0 = found at start, -1 or false = not found)
- `substr()`: Extract portion (start position, length)
- `explode()`: Break string into array at delimiter
- `implode()`: Join array elements with delimiter
- Comparison functions return 0 if equal

---

#### **Form Processing**
```html
<!-- HTML Form -->
<form method="POST" action="process.php">
    <input type="text" name="username" required>
    <input type="email" name="email" required>
    <input type="password" name="password" required>
    <input type="checkbox" name="terms"> Agree to terms
    <select name="country">
        <option>India</option>
        <option>USA</option>
    </select>
    <button type="submit">Submit</button>
</form>

<!-- process.php -->
<?php
// Check if form was submitted
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    // Get form data (null coalescing operator ?? returns default if key missing)
    $username = $_POST["username"] ?? "";
    $email = $_POST["email"] ?? "";
    $password = $_POST["password"] ?? "";
    $terms = isset($_POST["terms"]) ? "Yes" : "No";  // Check if checkbox checked
    $country = $_POST["country"] ?? "";
    
    // Validate data
    if (empty($username) || empty($email)) {
        echo "All fields required";
    } else if (!filter_var($email, FILTER_VALIDATE_EMAIL)) {
        echo "Invalid email";
    } else {
        echo "Form submitted successfully";
        // Process data: insert into database, send email, etc.
    }
}
?>
```

**Code Explanation**:
- `$_POST`: Global array containing form data (only if method="POST")
- `$_SERVER["REQUEST_METHOD"]`: Check if request is POST or GET
- `?? ""`: Null coalescing operator (value if exists, empty string otherwise)
- `isset()`: Check if variable/key exists
- `empty()`: Check if empty (false, 0, "", null, etc.)
- `filter_var()`: Validate using filter (FILTER_VALIDATE_EMAIL for email)
- Security: Always validate/sanitize user input

---

#### **Database Connection**
```php
<?php
// MySQLi Procedural
$connection = mysqli_connect("localhost", "user", "password", "database");
if (!$connection) {
    die("Connection failed: " . mysqli_connect_error());
}

// MySQLi Object-oriented
$mysqli = new mysqli("localhost", "user", "password", "database");
if ($mysqli->connect_error) {
    die("Connection failed: " . $mysqli->connect_error);
}

// PDO (Recommended - modern, more secure)
$pdo = new PDO("mysql:host=localhost;dbname=database", "user", "password");
$pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);

// Close connections
mysqli_close($connection);
$mysqli->close();
// PDO closes automatically when object destroyed
?>
```

**How Database Connection Works**:
- Establishes link between PHP and database
- Credentials: hostname (localhost), username, password, database name
- Error checking: If connection fails, display error message
- PDO preferred: Supports multiple databases, prepared statements prevent SQL injection

---

#### **Basic Database Operations**

**INSERT - Add new data**:
```php
<?php
$pdo = new PDO("mysql:host=localhost;dbname=mydb", "user", "pass");

// Prepared statement (safe from SQL injection)
$stmt = $pdo->prepare("INSERT INTO users (name, email, age) VALUES (:name, :email, :age)");
$stmt->execute([
    ':name' => 'John',
    ':email' => 'john@example.com',
    ':age' => 25
]);

echo "Record inserted successfully";
echo "ID: " . $pdo->lastInsertId();  // Get auto-increment ID
?>
```

**How It Works**:
- `prepare()`: Create statement template (? or :name for placeholders)
- `execute()`: Replace placeholders with actual values
- Placeholders prevent SQL injection (malicious code)
- `lastInsertId()`: Get ID of newly inserted row

---

**SELECT - Retrieve data**:
```php
<?php
$pdo = new PDO("mysql:host=localhost;dbname=mydb", "user", "pass");

// Fetch all records
$stmt = $pdo->prepare("SELECT * FROM users WHERE age > :age");
$stmt->execute([':age' => 20]);
$users = $stmt->fetchAll(PDO::FETCH_ASSOC);  // All rows as array

foreach ($users as $user) {
    echo $user['name'] . " - " . $user['email'] . "<br>";
}

// Fetch single record
$stmt = $pdo->prepare("SELECT * FROM users WHERE id = :id");
$stmt->execute([':id' => 1]);
$user = $stmt->fetch(PDO::FETCH_ASSOC);  // One row

echo $user['name'];
?>
```

**Code Explanation**:
- `SELECT`: Retrieve data
- `WHERE`: Filter conditions
- `fetchAll()`: Get all matching rows as array
- `fetch()`: Get first matching row
- `PDO::FETCH_ASSOC`: Return as associative array (key=>value)
- Loop through results and display

---

**UPDATE - Modify existing data**:
```php
<?php
$pdo = new PDO("mysql:host=localhost;dbname=mydb", "user", "pass");

$stmt = $pdo->prepare("UPDATE users SET age = :age WHERE id = :id");
$stmt->execute([
    ':age' => 26,
    ':id' => 1
]);

echo $stmt->rowCount() . " records updated";  // Number affected
?>
```

**Code Explanation**:
- `UPDATE`: Modify data
- `SET`: What to change
- `WHERE`: Which rows to change
- `rowCount()`: How many rows affected

---

**DELETE - Remove data**:
```php
<?php
$pdo = new PDO("mysql:host=localhost;dbname=mydb", "user", "pass");

$stmt = $pdo->prepare("DELETE FROM users WHERE id = :id");
$stmt->execute([':id' => 1]);

echo $stmt->rowCount() . " records deleted";  // Number affected
?>
```

**Code Explanation**:
- `DELETE FROM`: Remove rows
- `WHERE`: Which rows to delete
- `rowCount()`: How many rows deleted

---

#### **Setting Query Parameters**
```php
<?php
// Named Parameters (recommended - clearer)
$stmt = $pdo->prepare("SELECT * FROM users WHERE name = :name AND age > :age");
$stmt->execute([
    ':name' => 'John',
    ':age' => 20
]);

// Positional Parameters (? instead of :name)
$stmt = $pdo->prepare("SELECT * FROM products WHERE price > ? AND category = ?");
$stmt->execute([100, 'Electronics']);
// Parameters in order they appear
?>
```

**Code Explanation**:
- Named parameters: `:name` - clearer what each value is
- Positional parameters: `?` - values in order of ?
- Named preferred: More readable, less error-prone

---

#### **SQL Joins**

**INNER JOIN - Only matching records from both tables**:
```php
<?php
$sql = "SELECT users.name, orders.product 
        FROM users 
        INNER JOIN orders ON users.id = orders.user_id";
$stmt = $pdo->prepare($sql);
$stmt->execute();
$results = $stmt->fetchAll();
// Only returns users who have orders
?>
```

---

**LEFT JOIN - All from left table + matching from right**:
```php
<?php
$sql = "SELECT users.name, orders.product 
        FROM users 
        LEFT JOIN orders ON users.id = orders.user_id";
// Returns all users, even without orders (NULL for products)
?>
```

---

**RIGHT JOIN - All from right table + matching from left**:
```php
<?php
$sql = "SELECT users.name, orders.product 
        FROM users 
        RIGHT JOIN orders ON users.id = orders.user_id";
// Returns all orders, even without matching users
?>
```

---

**CROSS JOIN - Cartesian product (all combinations)**:
```php
<?php
$sql = "SELECT * FROM table1 CROSS JOIN table2";
// Returns every row from table1 with every row from table2
?>
```

---

**SELF JOIN - Join table with itself**:
```php
<?php
$sql = "SELECT a.name, b.name 
        FROM employees a, employees b 
        WHERE a.manager_id = b.id";
// a and b are aliases for same table
// Finds employees and their managers
?>
```

---

#### **Cookies and Sessions**

**Cookies - Data stored on client**:
```php
<?php
// Set cookie (persists across requests)
setcookie("username", "John", time() + 3600, "/");
// Parameters: name, value, expiration (time + seconds), path

// Retrieve cookie
echo $_COOKIE["username"];  // "John"

// Delete cookie (set expiration to past)
setcookie("username", "", time() - 3600, "/");

// Check if exists
if (isset($_COOKIE["username"])) {
    echo $_COOKIE["username"];
} else {
    echo "Not logged in";
}

// Note: setcookie() must be before any output
?>
```

**Code Explanation**:
- Cookies: Stored on user's computer, sent with every request
- `setcookie()`: Create/modify cookie
- `time() + 3600`: Expiration (now + 1 hour in seconds)
- `$_COOKIE`: Access cookies
- Must call before sending output to browser

---

**Sessions - Data stored on server**:
```php
<?php
// Start session (must be first in script)
session_start();

// Set session variable (stored on server)
$_SESSION["username"] = "John";
$_SESSION["user_id"] = 123;
$_SESSION["role"] = "admin";

// Retrieve session variable (available on all pages if session_start() called)
echo $_SESSION["username"];  // "John"

// Unset specific variable
unset($_SESSION["username"]);

// Destroy entire session (logout)
session_destroy();

// Check if logged in
if (isset($_SESSION["user_id"])) {
    echo "Welcome " . $_SESSION["username"];
} else {
    echo "Not logged in";
}
?>
```

**How Sessions Work**:
- Server creates session ID (unique code)
- Session ID sent to client (in cookie or URL)
- Client sends session ID back with each request
- Server uses ID to retrieve stored data
- More secure than cookies (data on server, not client)
- Lifetime: Expires when user closes browser or server timeout

---

#### **Accessing Database Data into HTML**
```php
<?php
session_start();
$pdo = new PDO("mysql:host=localhost;dbname=mydb", "user", "pass");

// Get data from database
$stmt = $pdo->prepare("SELECT * FROM products WHERE category = :category LIMIT 10");
$stmt->execute([':category' => $_GET['category'] ?? 'Electronics']);
$products = $stmt->fetchAll(PDO::FETCH_ASSOC);
?>

<!DOCTYPE html>
<html>
<head><title>Products</title></head>
<body>
<h1>Our Products</h1>
<table border="1">
    <tr>
        <th>ID</th>
        <th>Name</th>
        <th>Price</th>
        <th>Category</th>
    </tr>
    <?php foreach ($products as $product): ?>
    <tr>
        <td><?= htmlspecialchars($product['id']) ?></td>
        <td><?= htmlspecialchars($product['name']) ?></td>
        <td>$<?= htmlspecialchars($product['price']) ?></td>
        <td><?= htmlspecialchars($product['category']) ?></td>
    </tr>
    <?php endforeach; ?>
</table>
</body>
</html>
```

**How It Works**:
- PHP code at top: Query database, get data
- HTML below: Display data in table
- `<?=` is shorthand for `<?php echo`
- `htmlspecialchars()`: Escape HTML (prevent XSS attacks)
- Mixes PHP and HTML seamlessly

---

## UNIT IV: AJAX and PHP Integration

### **AJAX Introduction**

**Definition**: AJAX (Asynchronous JavaScript and XML) allows updating web pages asynchronously without full page reload.

---

#### **Creating Simple AJAX Application**
```html
<!DOCTYPE html>
<html>
<head>
    <title>Simple AJAX App</title>
    <style>
        #result { border: 1px solid #ccc; padding: 10px; margin-top: 10px; }
    </style>
</head>
<body>
    <h1>Load Content via AJAX</h1>
    <button onclick="loadContent()">Load Data</button>
    <div id="result"></div>

    <script>
        function loadContent() {
            // Create XMLHttpRequest object
            const xhr = new XMLHttpRequest();
            
            // Configure request
            xhr.open('GET', 'data.php', true);
            
            // Handle response when data received
            xhr.onload = function() {
                if (xhr.status === 200) {
                    // Success: put data in div
                    document.getElementById('result').innerHTML = xhr.responseText;
                }
            };
            
            // Handle errors
            xhr.onerror = function() {
                console.error('Request failed');
            };
            
            // Send request to server
            xhr.send();
        }
    </script>
</body>
</html>
```

**How It Works - General Overview**:
Button click triggers function. Function creates XMLHttpRequest, sends to server, waits for response, updates page without reload.

**Component Breakdown**:
- `new XMLHttpRequest()`: Create object to communicate with server
- `xhr.open('GET', 'data.php', true)`: Configure request
  - `'GET'`: HTTP method (retrieve data)
  - `'data.php'`: URL to request
  - `true`: Asynchronous (don't wait, continue execution)
- `xhr.onload`: Function runs when response received
- `xhr.status === 200`: Check if successful (200 = OK)
- `xhr.responseText`: Data received from server (as string)
- `xhr.send()`: Send request

---

#### **XMLHttpRequest Object**
```javascript
// Create XMLHttpRequest object
const xhr = new XMLHttpRequest();

// Configure request (open method)
xhr.open(method, url, async);
// method: GET (retrieve), POST (send), PUT, DELETE, etc.
// url: Server endpoint
// async: true (non-blocking) or false (blocking)

// Set request headers (optional)
xhr.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");

// Handle ready state changes (connection lifecycle)
xhr.onreadystatechange = function() {
    // readyState: 0(uninitialized), 1(loading), 2(loaded), 3(interactive), 4(complete)
    // status: 200(OK), 404(Not Found), 500(Server Error)
    if (xhr.readyState === 4 && xhr.status === 200) {
        const response = xhr.responseText;
        // Process response
    }
};

// Alternate: onload (runs when transfer complete)
xhr.onload = function() {
    if (xhr.status === 200) {
        const response = xhr.responseText;
    }
};

// Send request
xhr.send();
// For POST: xhr.send("data=value&name=John");

// Abort request if needed
xhr.abort();

// Response properties
xhr.responseText;   // Response as plain text
xhr.responseXML;    // Response as XML document
xhr.status;         // HTTP status code
xhr.statusText;     // HTTP status text ("OK", "Not Found")
xhr.getAllResponseHeaders(); // All response headers
```

**Code Explanation**:
- `open()`: Set up request (doesn't send yet)
- `setRequestHeader()`: Add header info
- `onreadystatechange`: Fires multiple times as request progresses
- `readyState 4`: Transfer complete (data ready)
- `status 200`: Success
- `responseText`: String data from server
- `responseXML`: XML data from server
- `send()`: Actually send request to server

---

#### **AJAX vs Non-AJAX Applications**

**Non-AJAX (Traditional)**:
```
User Action → Form Submission → Page Reload → Server Response → Display New Page
Problem: Entire page refreshes (slow, user waits, content flickers)
```

**AJAX**:
```
User Action → XMLHttpRequest → Server Response → Update Partial DOM → No Page Reload
Benefit: Faster (only data loaded, not HTML), smoother (no flicker), responsive
```

---

#### **Working with PHP and AJAX**

**Frontend (HTML + JavaScript)**:
```html
<!DOCTYPE html>
<html>
<head>
    <title>AJAX with PHP</title>
</head>
<body>
    <h1>User Search</h1>
    <input type="text" id="searchInput" placeholder="Enter name">
    <button onclick="searchUsers()">Search</button>
    <div id="results"></div>

    <script>
        function searchUsers() {
            const query = document.getElementById('searchInput').value;
            
            const xhr = new XMLHttpRequest();
            xhr.open('POST', 'search.php', true);
            xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
            
            xhr.onload = function() {
                if (xhr.status === 200) {
                    // Display results from server
                    document.getElementById('results').innerHTML = xhr.responseText;
                }
            };
            
            // Send search query to server
            xhr.send('query=' + encodeURIComponent(query));
        }
    </script>
</body>
</html>
```

**Backend (PHP)**:
```php
<?php
// search.php
$query = $_POST['query'] ?? '';

// Connect to database
$pdo = new PDO("mysql:host=localhost;dbname=mydb", "user", "pass");

// Search database for matching names
$stmt = $pdo->prepare("SELECT id, name, email FROM users WHERE name LIKE :query");
$stmt->execute([':query' => '%' . $query . '%']);  // % for wildcard
$results = $stmt->fetchAll(PDO::FETCH_ASSOC);

// Generate HTML response
if ($results) {
    echo '<ul>';
    foreach ($results as $user) {
        echo '<li>' . htmlspecialchars($user['name']) . ' - ' . htmlspecialchars($user['email']) . '</li>';
    }
    echo '</ul>';
} else {
    echo '<p>No users found</p>';
}
?>
```

**How It Works Together**:
- User types in input
- JavaScript gets input value and sends to server via XMLHttpRequest
- Server (PHP) receives query, searches database
- Server generates HTML list of results
- Server sends HTML back to JavaScript
- JavaScript displays HTML in results div
- All without page reload

---

#### **Processing Client Requests**
```php
<?php
// Determine HTTP method and handle accordingly
if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    $action = $_POST['action'] ?? '';
    
    // Route to appropriate function
    switch ($action) {
        case 'add':
            $result = addUser($_POST);  // Call add function
            break;
        case 'delete':
            $result = deleteUser($_POST['id']);  // Call delete function
            break;
        default:
            $result = ['error' => 'Unknown action'];
    }
    
    // Send JSON response (standard for AJAX)
    header('Content-Type: application/json');
    echo json_encode($result);  // Convert array to JSON string
    
} else if ($_SERVER['REQUEST_METHOD'] === 'GET') {
    $id = $_GET['id'] ?? '';
    $user = getUser($id);  // Get user data
    
    header('Content-Type: application/json');
    echo json_encode($user);  // Send as JSON
}

// Helper functions
function addUser($data) {
    // Validate and insert
    return ['success' => true, 'message' => 'User added'];
}

function deleteUser($id) {
    // Delete from database
    return ['success' => true, 'message' => 'User deleted'];
}

function getUser($id) {
    // Query database
    return ['id' => $id, 'name' => 'John', 'email' => 'john@example.com'];
}
?>
```

**Code Explanation**:
- `$_SERVER['REQUEST_METHOD']`: Check if POST or GET
- `$_POST/$_GET['key']`: Get data from client
- Routes different actions to different functions
- `header()`: Set response type to JSON
- `json_encode()`: Convert array to JSON (universal format)
- Organized structure: Easy to add more actions

---

#### **Accessing Files Using PHP**
```php
<?php
// file_get_contents - Read entire file
$data = file_get_contents('data.txt');
echo $data;

// file_put_contents - Write to file
file_put_contents('data.txt', 'New content');
file_put_contents('log.txt', "Event: " . date('Y-m-d H:i:s') . "\n", FILE_APPEND);

// file - Read file into array (line by line)
$lines = file('data.txt');
foreach ($lines as $line) {
    echo $line . "<br>";
}

// readfile - Output file directly (useful for downloads)
readfile('document.pdf');

// fopen, fread, fclose - Manual file handling
$file = fopen('data.txt', 'r');  // 'r' = read mode
$content = fread($file, filesize('data.txt'));  // Read all bytes
fclose($file);  // Always close

// scandir - List files in directory
$files = scandir('folder/');
foreach ($files as $file) {
    echo $file . '<br>';  // Each filename
}

// file_exists - Check if file exists
if (file_exists('config.php')) {
    include 'config.php';
}

// is_dir - Check if path is directory
// is_file - Check if path is file
?>
```

**Code Explanation**:
- `file_get_contents()`: Read entire file (simple)
- `file_put_contents()`: Write to file (overwrites or appends)
- `FILE_APPEND`: Flag to append instead of overwrite
- `file()`: Read into array (each line is element)
- `fopen()`: Open file with mode ('r'=read, 'w'=write, 'a'=append)
- `fread()`: Read specified bytes
- `fclose()`: Close file handle
- `filesize()`: Get file size in bytes
- `scandir()`: List directory contents

---

#### **Implementing Security and Accessibility in AJAX**

**Security in AJAX**:
```php
<?php
// 1. Validate and sanitize input
$input = filter_var($_POST['data'], FILTER_SANITIZE_STRING);

// 2. Use prepared statements (prevent SQL injection)
$stmt = $pdo->prepare("SELECT * FROM users WHERE id = :id");
$stmt->execute([':id' => $id]);

// 3. Implement CSRF protection
session_start();
if ($_POST['csrf_token'] !== $_SESSION['csrf_token']) {
    http_response_code(403);
    die('CSRF token mismatch');
}

// 4. Use HTTPS for all communications (encrypt data)
if (empty($_SERVER['HTTPS'])) {
    header('Location: https://' . $_SERVER['HTTP_HOST'] . $_SERVER['REQUEST_URI']);
    exit;
}

// 5. Validate file uploads (size, type)
if ($_FILES['file']['size'] > 5000000) {  // 5MB limit
    die('File too large');
}

// 6. Check file type (whitelist safe types)
$allowed = ['jpg', 'png', 'gif'];
$ext = pathinfo($_FILES['file']['name'], PATHINFO_EXTENSION);
if (!in_array($ext, $allowed)) {
    die('File type not allowed');
}

// 7. Store sensitive data server-side only (not in client-side JavaScript)
// 8. Implement rate limiting (prevent brute force)
// 9. Log security events (track suspicious activity)
?>
```

**Code Explanation**:
- `FILTER_SANITIZE_STRING`: Remove dangerous characters
- Prepared statements: Placeholders prevent SQL injection
- CSRF tokens: Prevent cross-site attacks
- HTTPS: Encrypt all data transmission
- File validation: Size and type checks
- Whitelist: Only allow specific file types
- Rate limiting: Limit requests per time period
- Logging: Track suspicious activity

---

**Accessibility in AJAX**:
```html
<!DOCTYPE html>
<html>
<head>
    <title>Accessible AJAX</title>
</head>
<body>
    <!-- Use semantic HTML -->
    <main>
        <form id="searchForm">
            <label for="searchInput">Search:</label>
            <input type="search" id="searchInput" aria-label="Search for users" required>
            <button type="submit" aria-label="Search">Search</button>
        </form>
        
        <!-- ARIA live region - announces updates to screen readers -->
        <div id="results" aria-live="polite" aria-atomic="true" role="region">
            <!-- Results will be loaded here -->
        </div>
    </main>

    <script>
        document.getElementById('searchForm').onsubmit = function(e) {
            e.preventDefault();
            
            // Announce loading to screen readers
            document.getElementById('results').textContent = 'Loading results...';
            
            const xhr = new XMLHttpRequest();
            xhr.open('POST', 'search.php', true);
            
            xhr.onload = function() {
                if (xhr.status === 200) {
                    // Results updated - screen reader announces automatically
                    document.getElementById('results').innerHTML = xhr.responseText;
                }
            };
            
            xhr.send('query=' + encodeURIComponent(document.getElementById('searchInput').value));
        };
    </script>
</body>
</html>
```

**Code Explanation**:
- Semantic HTML: `<main>`, `<form>`, `<label>` for structure
- `aria-label`: Describes element for screen readers
- `aria-live="polite"`: Region announces changes (not interrupting)
- `aria-atomic="true"`: Announce entire region change
- `role="region"`: Identifies important area
- Update announcement: Screen readers announce dynamically loaded content

---

#### **Modern Alternative: Fetch API** (instead of XMLHttpRequest)

```javascript
// Fetch is modern, promise-based, cleaner syntax
fetch('data.php', {
    method: 'POST',  // HTTP method
    headers: {
        'Content-Type': 'application/json'  // Tell server format
    },
    body: JSON.stringify({  // Convert object to JSON
        name: 'John',
        email: 'john@example.com'
    })
})
.then(response => response.json())  // Parse response as JSON
.then(data => {
    console.log('Success:', data);
    document.getElementById('results').innerHTML = data;
})
.catch(error => console.error('Error:', error));  // Handle errors
```

**Why Fetch is Better**:
- Promise-based (cleaner than callbacks)
- Simpler syntax
- Built-in JSON support
- Better error handling
- Modern standard (supported by all browsers now)

---

## FINAL EXAMINATION TIPS

### Study Recommendations:
1. **HTML5**: Focus on semantic elements, forms, multimedia tags, accessibility
2. **CSS3**: Understand Flexbox, Grid, positioning, animations, responsive design, media queries
3. **JavaScript**: Master DOM manipulation, event handling, arrays, functions, objects, async operations
4. **PHP**: Database operations, form processing, security practices, file handling
5. **AJAX**: Client-server communication, asynchronous requests, JSON/XML data exchange, security
6. **Bootstrap**: Grid system, components, responsive utilities, customization

### Common Exam Questions:
1. Explain MVC architecture in web development
2. Difference between GET and POST methods
3. SQL injection prevention methods
4. DOM vs SAX parsing in XML
5. Same-origin policy and CORS
6. Session vs Cookie differences
7. Event bubbling and event delegation
8. Async vs Defer in script loading
9. RESTful API principles
10. Responsive design techniques

### Practice Questions:
1. Create a registration form with HTML5 validation
2. Style a webpage with CSS3 animations and transitions
3. Write JavaScript to validate form data before submission
4. Connect to MySQL database with PHP and execute CRUD operations
5. Implement AJAX search functionality
6. Secure PHP code against SQL injection
7. Design responsive Bootstrap layout for mobile and desktop
8. Implement file upload and validation in PHP
9. Create a dynamic table that loads data via AJAX
10. Build a complete web application using HTML, CSS, JavaScript, PHP, and MySQL

### Time Management in Exam:
- Allocate 20% time to read and understand all questions
- Allocate 70% time to coding/writing answers
- Allocate 10% time to review and verification
- Answer comprehensive questions first (more marks)
- Show your code logic even if incomplete

### Scoring High:
- Write clean, well-commented code
- Follow best practices and security standards
- Include error handling in code
- Provide multiple approaches if possible
- Explain your code with comments
- Test your code mentally before submitting

---

**Good Luck for Your Final Examination!**
