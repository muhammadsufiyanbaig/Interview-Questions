## **5. Next.js**

---

### **Beginner:**

**1. What is Next.js, and how does it differ from React?**  
Next.js is a React framework that enables functionalities such as server-side rendering and static site generation. While React is a library for building user interfaces, Next.js provides a robust structure and additional features to build full-fledged web applications.

---

**2. What are the key features of Next.js?**  
- **File-based Routing:** Automatic routing based on the file system.
- **Server-side Rendering (SSR):** Pre-renders pages on each request.
- **Static Site Generation (SSG):** Pre-renders pages at build time.
- **API Routes:** Create backend endpoints within the application.
- **Built-in CSS Support:** Import CSS files and use CSS modules.
- **Image Optimization:** Automatic image optimization with the `next/image` component.

---

**3. Explain file-based routing in Next.js.**  
Next.js uses the file system to define routes. Each file in the `pages` directory automatically becomes a route. For example, `pages/index.js` maps to the homepage, and `pages/about.js` maps to `/about`.

---

**4. How do you create dynamic routes in Next.js?**  
Dynamic routes are created by using square brackets in the filename within the `pages` directory. For example, `pages/post/[id].js` creates a dynamic route that can be accessed with `/post/1`, `/post/2`, etc.

---

**5. What is the difference between client-side rendering (CSR) and server-side rendering (SSR)?**  
- **Client-side Rendering (CSR):** The browser downloads a minimal HTML page and JavaScript, then renders the content on the client-side.
- **Server-side Rendering (SSR):** The server generates the full HTML for a page on each request and sends it to the client, improving performance and SEO.

---

**6. What are API routes in Next.js?**  
API routes allow you to create server-side endpoints within your Next.js application. By adding files to the `pages/api` directory, you can define functions that handle HTTP requests and responses.

---

**7. How does `getStaticProps()` work?**  
`getStaticProps` is a Next.js function that allows you to fetch data at build time. It pre-renders the page with the fetched data, enabling static site generation.

---

**8. What is the purpose of `getServerSideProps()`?**  
`getServerSideProps` is used to fetch data on each request. It enables server-side rendering by fetching data at request time and passing it to the page component.

---

**9. What is Incremental Static Regeneration (ISR) in Next.js?**  
ISR allows you to update static content after deployment without rebuilding the entire site. By setting a `revalidate` time in `getStaticProps`, Next.js will regenerate the page in the background at the specified interval.

---

**10. How do you use `next/image` for optimized images?**  
The `next/image` component provides automatic image optimization. It requires specifying the `src`, `width`, and `height` properties, and it supports lazy loading and responsive images.

---

### **Mid-Level:**

**1. How does Next.js handle static site generation (SSG)?**  
Next.js pre-renders pages at build time using `getStaticProps`. It generates static HTML files that can be served directly, improving performance and enabling CDN caching.

---

**2. Explain how to use middleware in Next.js.**  
Middleware in Next.js can be implemented using custom server setups or API routes. It allows you to run code before a request is completed, enabling tasks like authentication and request logging.

---

**3. What are the benefits of using `getInitialProps()`?**  
`getInitialProps` is used to fetch data on the server before rendering a page. It enables server-side rendering and can also run on the client during navigation. However, it's recommended to use `getStaticProps` or `getServerSideProps` in newer versions of Next.js.

---

**4. How do you handle authentication in Next.js?**  
Authentication can be handled using API routes to manage login sessions, integrating authentication libraries like NextAuth.js, or using middleware to protect specific routes.

---

**5. How do you optimize SEO in Next.js applications?**  
- Use the `Head` component to manage meta tags.
- Implement server-side rendering or static site generation for content.
- Use semantic HTML and proper heading structures.
- Optimize images and ensure fast load times.

---

**6. How does Next.js handle API caching?**  
Next.js allows caching strategies through the use of `Cache-Control` headers in API routes. You can set these headers to control how responses are cached by browsers and CDNs.

---

**7. How do you manage environment variables in Next.js?**  
Environment variables can be managed using `.env` files. Next.js supports `.env.local`, `.env.development`, and `.env.production` files. Variables prefixed with `NEXT_PUBLIC_` are exposed to the browser.

---

**8. What are middleware functions in Next.js, and how do they work?**  
Middleware functions intercept requests before they reach the final handler. In Next.js, they can be implemented in API routes or custom servers to perform tasks like authentication, logging, or request modification.

---

**9. How do you implement internationalization (i18n) in Next.js?**  
Next.js has built-in support for internationalized routing. You can define locales, default locales, and domain-specific locales in the `next.config.js` file.

---

**10. How do you integrate Next.js with Redux or Zustand?**  
To integrate state management libraries like Redux or Zustand, wrap your application with the respective provider in `_app.js` and configure the store accordingly.

---


### **Senior-Level:**

**6. How do you handle role-based access control (RBAC) in Next.js?**  
RBAC can be implemented using a combination of authentication and authorization strategies:
- Store user roles in a JWT or session.
- Use middleware or logic in `getServerSideProps()`/API routes to check permissions.
- Protect frontend components by conditionally rendering based on role.
- Use `next-auth` or custom auth to store and manage user roles securely.

---

**7. How do you use Next.js with Vercel for seamless deployment?**  
Vercel is the platform created by the creators of Next.js and offers native support:
- Connect your GitHub repo to Vercel.
- Push changes to the repo → Vercel builds and deploys automatically.
- Vercel supports automatic static optimization, serverless functions, and environment variables.
- Supports preview deployments for PRs and production/staging environments out-of-the-box.

---

**8. What are the differences between `getStaticProps()` and `getServerSideProps()`?**  
| Feature                | `getStaticProps()`            | `getServerSideProps()`        |
|------------------------|-------------------------------|-------------------------------|
| When it runs           | At **build time**             | On **every request**          |
| Performance            | Faster (static HTML served)   | Slightly slower (SSR on each request) |
| Use case               | Blogs, documentation, static pages | User-specific dashboards, auth-protected pages |
| Revalidation support   | Yes (`revalidate`)            | No (new request every time)   |

---

**9. How do you implement a microservices architecture in a Next.js application?**  
You can split functionality across services:
- Each service (auth, user, content, etc.) has its own backend/API.
- Next.js consumes these APIs via `getServerSideProps()`, `getStaticProps()`, or client-side fetching.
- Use technologies like API Gateway, service discovery, and centralized logging.
- Use Docker or Kubernetes for container orchestration if scaling horizontally.

---

**10. How do you handle complex caching strategies in Next.js?**  
Next.js supports various levels of caching:
- **Static Generation:** Built at compile time, cached at CDN.
- **ISR (Incremental Static Regeneration):** Revalidate pages on demand with `revalidate`.
- **API Route Caching:** Set custom `Cache-Control` headers.
- **Middleware/Edge Caching:** Use edge functions with headers or cookies.
- **External CDN (e.g., Cloudflare):** Use for full-page caching and cache purging.

Example for `Cache-Control` header in API route:
```js
res.setHeader('Cache-Control', 's-maxage=60, stale-while-revalidate');
```
