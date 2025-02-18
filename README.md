# Nexa Blog - Next.js Blogging Platform

## 🚀 Overview
Nexa Blog is a modern, full-stack blogging platform built with **Next.js**, leveraging **Server Actions**, **Server-Side Rendering (SSR)**, **Static Site Generation (SSG)**, **Route Handlers**, and **RTK Query** for client-side data fetching. The project follows best practices for performance, caching, and metadata generation.

## 📂 Project Structure
```
📦 nexablog
├── 📁 src
│   ├── 📁 app
│   │   ├── 📁 blogs
│   │   │   ├── 📁 [blogId]  # Dynamic routes for individual blog pages
│   │   │   │   ├── 📄 page.tsx
│   │   │   │   ├── 📄 route.ts
│   │   │   │   ├── 📄 metadata.ts
│   │   ├── 📄 page.tsx  # Homepage
│   ├── 📁 components  # Reusable UI components
│   ├── 📁 actions  # Server actions like creating blogs
│   ├── 📁 types  # TypeScript interfaces
├── 📄 package.json
├── 📄 README.md
├── 📄 next.config.js
```

## ⚙️ Features
✅ **Server Actions** - Mutate and create blog posts asynchronously.
✅ **Server-Side Rendering (SSR)** - Fetch latest blogs dynamically.
✅ **Static Site Generation (SSG)** - Pre-generate blog pages for better performance.
✅ **Route Handlers** - RESTful API endpoints with Next.js route handling.
✅ **Client-Side Data Fetching (RTK Query)** - Efficient blog data fetching.
✅ **Dynamic Metadata** - SEO-friendly metadata for each blog page.
✅ **Caching & Revalidation** - Optimized content refresh for performance.

---

## 🛠 Technologies Used
- **Next.js 14**
- **TypeScript**
- **Tailwind CSS**
- **RTK Query (Redux Toolkit Query)**
- **REST API with Route Handlers**
- **Server Actions & Mutations**

---

## 🏗️ Setup & Installation

### 1️⃣ Clone the repository
```sh
git clone https://github.com/Apollo-Level2-Web-Dev/nexa-blog-starter-pack.git
cd nexablog
```

### 2️⃣ Install dependencies
```sh
npm install
```

### 3️⃣ Start the development server
```sh
npm run dev
```
The app will run at `http://localhost:3000`

### 4️⃣ Run the backend server (if applicable)
Ensure you have the backend API running on `http://localhost:5000`

---

## 🔥 Key Functionalities
### 🏠 Homepage (`/`)
- Displays the latest blogs with **caching & revalidation** (30s refresh cycle).

```tsx
const res = await fetch("http://localhost:5000/blogs", {
  next: { revalidate: 30 },
});
```

### 📄 Blog Details Page (`/blogs/[blogId]`)
- Retrieves blog data dynamically using **SSR**.

```tsx
const res = await fetch(`http://localhost:5000/blogs/${blogId}`);
```

### 📌 Static Generation (`generateStaticParams()`)
- Pre-generates static pages for performance.

```tsx
export const generateStaticParams = async () => {
  const res = await fetch("http://localhost:5000/blogs");
  const blogs = await res.json();
  return blogs.slice(0, 3).map((blog) => ({ blogId: blog.id }));
};
```

### ✍️ Create Blog Post (Server Actions)
- Uses **server-side form submission** with a POST request.

```tsx
export const createBlog = async (data: FormData) => {
  const blogData = Object.fromEntries(data.entries());
  const res = await fetch("http://localhost:5000/blogs", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(blogData),
  });
  return res.json();
};
```

### 🌍 API Route Handlers (`route.ts`)
- Implements **RESTful API endpoints**.

```tsx
export const GET = async (
    request: Request,
    { params }: { params: { id: string } }
) => {
    const { id } = await params;
    const blog = blogs.find((blog) => blog.id === id);
    return NextResponse.json(blog);
};
```

### ⚡ RTK Query (Client-Side Fetching)
- Uses **Redux Toolkit Query** for efficient data fetching.

```tsx
const { data: blogs, error, isLoading } = useGetBlogsQuery();
```

---

## 💡 Contribution Guidelines
We welcome contributions! Follow these steps:
1. **Fork** the repository.
2. **Create a branch** (`feature-new-blog`).
3. **Commit your changes** (`git commit -m "Added new feature"`).
4. **Push to GitHub** (`git push origin feature-new-blog`).
5. **Create a Pull Request**.


---

## 📞 Contact
For any inquiries, reach out at [rbiswas01999@gmail.com](mailto:rbiswas01999@gmail.com) 

# NexaBlog

## Installation:

1. Clone the repository.
2. Install dependencies using `npm install`.
3. Run the project using `npm run dev`.
