# Next.js Interview Q&A (Core Concepts)

---

## 1. What is Next.js?

**Answer:**  
Next.js is a **React framework** for building **server-side rendered (SSR) and statically generated (SSG) applications**.  
It provides routing, performance optimization, and built-in tooling for React apps.

**Visual:**  
```
Next.js
 ├─ Pages → Routing
 ├─ Data Fetching → SSR/SSG/ISR
 ├─ API Routes → Backend
 └─ Optimization → Image, Fonts, Performance
```

---

## 2. What are the benefits of using Next.js?

**Answer:**  
- SSR and SSG for faster initial load  
- Automatic code splitting  
- Built-in routing  
- API routes support  
- Image optimization  
- SEO friendly

---

## 3. What is the Pages Directory?

**Answer:**  
Files in `pages/` automatically become routes. Each `.js`/`.tsx` file maps to a URL.

```
pages/
 ├─ index.js       → /
 ├─ about.js       → /about
 └─ blog/[id].js   → /blog/:id
```

---

## 4. What is File-Based Routing?

**Answer:**  
Routing in Next.js is based on **file structure inside `pages/`**.  
Dynamic routes use `[param]` syntax.

```
pages/blog/[id].js → /blog/1, /blog/2
```

---

## 5. What are Dynamic Routes?

**Answer:**  
Routes where parts of the URL are dynamic (like `/blog/123`).

```
pages/blog/[slug].js
```

**Visual:**  
```
URL: /blog/hello-world
File: pages/blog/[slug].js
slug = "hello-world"
```

---

## 6. What are Nested Routes?

**Answer:**  
Folders inside `pages/` create nested routes.

```
pages/dashboard/settings.js → /dashboard/settings
```

---

## 7. What is SSR (Server-Side Rendering)?

**Answer:**  
Pages rendered on the server on each request.  
Useful for **dynamic content and SEO**.

```
export async function getServerSideProps(context) {
  return { props: { data: await fetchData() } };
}
```

**Visual:**  
```
Request → Server → Render Page → Send HTML → Browser
```

---

## 8. What is SSG (Static Site Generation)?

**Answer:**  
Pages generated **at build time**.  
Fast and cacheable.

```
export async function getStaticProps() {
  return { props: { data: await fetchData() } };
}
```

**Visual:**  
```
Build Time → HTML Generated → Served from CDN → Browser
```

---

## 9. What is ISR (Incremental Static Regeneration)?

**Answer:**  
SSG pages can be **regenerated after a set interval**.

```
export async function getStaticProps() {
  return { props: { data }, revalidate: 10 }; // Rebuild every 10s
}
```

**Visual:**  
```
Old Page → Request → Re-generate → Update Cache → Serve New Page
```

---

## 10. What is CSR (Client-Side Rendering) in Next.js?

**Answer:**  
Fetching data **after page loads** on the client.

```
useEffect(() => { fetch('/api/data'); }, []);
```

**Visual:**  
```
Initial HTML → Browser JS → Fetch Data → Render Content
```

---

## 11. Difference between SSR, SSG, ISR, and CSR

| Type | When Rendered | Use Case |
|------|---------------|----------|
| SSR  | Each request  | Dynamic, SEO |
| SSG  | Build time    | Static content |
| ISR  | Build + interval | Mostly static, some updates |
| CSR  | Client only   | Highly dynamic, user-specific |

---

## 12. What are API Routes?

**Answer:**  
Create backend endpoints in `pages/api/`.

```
pages/api/hello.js
export default function handler(req, res) {
  res.status(200).json({ message: "Hello API" });
}
```

**Visual:**  
```
Browser → /api/hello → Next.js API Route → Response
```

---

## 13. What is getStaticPaths?

**Answer:**  
Required for **dynamic SSG routes** to pre-render paths.

```
export async function getStaticPaths() {
  return { paths: [{ params: { id: '1' } }], fallback: false };
}
```

---

## 14. What is fallback in getStaticPaths?

**Answer:**  
- `false` → only pre-rendered paths are valid  
- `true` → render missing paths on first request  
- `'blocking'` → server renders missing path before sending response

---

## 15. What is the App Directory (Next.js 13+)?

**Answer:**  
New `app/` directory supports:  
- Nested layouts  
- Server components  
- Streaming & suspense  
- Enhanced routing

**Visual:**  
```
app/
 ├─ layout.js → common layout
 ├─ page.js   → main page
 └─ dashboard/
     ├─ layout.js
     └─ page.js
```

---

## 16. What are Server Components?

**Answer:**  
Render **on the server**. Cannot use client hooks (`useState`, `useEffect`).  
Faster & smaller client bundle.

---

## 17. What are Client Components?

**Answer:**  
Marked with `'use client'`. Can use React hooks and browser APIs.

```
'use client';
export default function ClientComp() { ... }
```

---

## 18. What is Link Component?

**Answer:**  
Used for **client-side navigation** (faster than `<a>`).

```
import Link from 'next/link';
<Link href="/about">About</Link>
```

**Visual:**  
```
Click → JS Router → Update URL → Render Component
```

---

## 19. What is Image Component?

**Answer:**  
Optimizes images automatically with lazy loading & resizing.

```
import Image from 'next/image';
<Image src="/logo.png" width={100} height={50} />
```

---

## 20. What is Head Component?

**Answer:**  
Modify document `<head>` for SEO.

```
import Head from 'next/head';
<Head><title>My Page</title></Head>
```

---

## 21. What is Middleware?

**Answer:**  
Runs **before request completes**, useful for auth, redirects, headers.

```
export function middleware(req) { ... }
```

---

## 22. What is Next.js Routing vs React Router?

**Answer:**  
- Next.js: file-based, built-in  
- React Router: manual, needs configuration

---

## 23. What is next.config.js?

**Answer:**  
Next.js config file for custom settings (images, rewrites, environment variables, etc.)

```
module.exports = { reactStrictMode: true };
```

---

## 24. What is API Route Middleware?

**Answer:**  
Intercepts API requests for auth, logging, validation.

---

## 25. What are Layouts in Next.js 13+?

**Answer:**  
Persistent UI sections across pages (header/footer).

**Visual:**  
```
Root Layout
 ├─ Header
 ├─ Content
 │   └─ Nested Layout
 └─ Footer
```

---

## 26. What is Streaming with Suspense?

**Answer:**  
Server components can stream HTML while fetching data for faster load.

---

## 27. What is Prefetching?

**Answer:**  
Next.js automatically preloads pages linked with `<Link>` for fast navigation.

---

## 28. What is Code Splitting?

**Answer:**  
Next.js splits JS bundles automatically per page to reduce load time.

---

## 29. What is getServerSideProps vs getStaticProps?

**Answer:**  
- `getServerSideProps` → runs **on each request**  
- `getStaticProps` → runs **at build time**  

**Visual:**  
```
Build → getStaticProps → HTML → CDN
Request → getServerSideProps → Server → HTML
```

---

## 30. What is fallback: 'blocking'?

**Answer:**  
For dynamic SSG pages, server waits for HTML generation before sending response.

---

## 31. What is next/link vs next/router?

**Answer:**  
- `next/link` → JSX component for navigation  
- `next/router` → programmatic navigation (push, replace)

```
import { useRouter } from 'next/router';
router.push('/about');
```

---

## 32. What is ISR’s advantage over SSR?

**Answer:**  
- SSG with periodic updates → faster than SSR  
- CDN cacheable

---

## 33. What are Environment Variables?

**Answer:**  
- `.env.local`, `.env.production`  
- Prefix with `NEXT_PUBLIC_` for client exposure

```
NEXT_PUBLIC_API_URL=https://api.example.com
```

---

## 34. What is next/image vs img?

**Answer:**  
- `next/image`: optimized, lazy-loaded, responsive  
- `img`: plain HTML, no optimization

---

## 35. What is next/font?

**Answer:**  
Automatic font optimization in Next.js 13+.

```
import { Inter } from 'next/font/google';
const inter = Inter({ subsets: ['latin'] });
```

---

## 36. What is next/script?

**Answer:**  
Load external JS scripts with strategies: `beforeInteractive`, `afterInteractive`, `lazyOnload`.

---

## 37. What is getInitialProps?

**Answer:**  
Legacy method for fetching data. Replaced by `getStaticProps` & `getServerSideProps`.

---

## 38. What is next/head vs app/layout.js head?

**Answer:**  
- `next/head`: per-page meta in pages directory  
- `layout.js`: new app directory head for all pages in layout

---

## 39. What are Redirects and Rewrites?

**Answer:**  
- Redirects → URL changes  
- Rewrites → URL masked but content served

```
module.exports = {
  async redirects() { return [{ source: '/old', destination: '/new', permanent: true }]; },
};
```

---

## 40. How to improve Next.js performance?

**Answer:**  
- Use SSG/ISR where possible  
- Optimize images & fonts  
- Prefetch pages  
- Minimize JS & CSS bundles  
- Use React.memo and lazy loading
