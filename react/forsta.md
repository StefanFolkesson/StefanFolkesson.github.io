För att skapa en ny React-app och skapa två till tre sidor där du kan skicka data mellan dem, följ dessa steg:

---

### 1. **Installera Node.js och npm**
Om du inte redan har Node.js och npm installerat:
- Ladda ner och installera från [Node.js officiella hemsida](https://nodejs.org).
- Kontrollera installationen:
  ```bash
  node -v
  npm -v
  ```

---

### 2. **Skapa en ny React-app**
Öppna en terminal och kör följande kommando:
```bash
npx create-react-app my-react-app
```
Detta skapar en ny React-projektmapp som heter `my-react-app`.

Gå in i mappen:
```bash
cd my-react-app
```

---

### 3. **Installera React Router**
React Router används för att skapa sidor och hantera navigering:
```bash
npm install react-router-dom
```

---

### 4. **Strukturera projektet**
Skapa en mappstruktur för dina sidor:
```
src/
├── components/
├── pages/
│   ├── Home.js
│   ├── About.js
│   ├── Contact.js
```

---

### 5. **Skapa sidorna**
#### `Home.js`
```jsx
import React from 'react';
import { Link } from 'react-router-dom';

function Home() {
  return (
    <div>
      <h1>Home Page</h1>
      <Link to="/about">Go to About</Link>
      <Link to="/contact">Go to Contact</Link>
    </div>
  );
}

export default Home;
```

#### `About.js`
```jsx
import React from 'react';
import { Link } from 'react-router-dom';

function About() {
  return (
    <div>
      <h1>About Page</h1>
      <Link to="/">Go to Home</Link>
    </div>
  );
}

export default About;
```

#### `Contact.js`
```jsx
import React, { useState } from 'react';
import { Link } from 'react-router-dom';

function Contact() {
  const [message, setMessage] = useState('');

  return (
    <div>
      <h1>Contact Page</h1>
      <textarea
        placeholder="Write a message"
        value={message}
        onChange={(e) => setMessage(e.target.value)}
      />
      <p>Your message: {message}</p>
      <Link to="/">Go to Home</Link>
    </div>
  );
}

export default Contact;
```

---

### 6. **Set up Routing**
Öppna `src/App.js` och ersätt innehållet med följande:
```jsx
import React from 'react';
import { BrowserRouter as Router, Routes, Route } from 'react-router-dom';
import Home from './pages/Home';
import About from './pages/About';
import Contact from './pages/Contact';

function App() {
  return (
    <Router>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="/contact" element={<Contact />} />
      </Routes>
    </Router>
  );
}

export default App;
```

---

### 7. **Starta utvecklingsservern**
Kör följande kommando i terminalen:
```bash
npm start
```

---

### 8. **Skicka data mellan sidor**
Om du vill skicka data mellan sidor kan du använda **URL-parametrar** eller **React Context API**.

#### Exempel med URL-parametrar:
Uppdatera `Link` i `Home.js`:
```jsx
<Link to="/contact?message=Hello!">Go to Contact</Link>
```

Hämta parametern i `Contact.js`:
```jsx
import { useLocation } from 'react-router-dom';

function Contact() {
  const location = useLocation();
  const params = new URLSearchParams(location.search);
  const message = params.get('message') || '';

  return (
    <div>
      <h1>Contact Page</h1>
      <p>Message from Home: {message}</p>
      <Link to="/">Go to Home</Link>
    </div>
  );
}
```
