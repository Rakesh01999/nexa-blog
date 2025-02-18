Here's a detailed README file for your Next.js project, incorporating the information and structure you've provided:

```markdown
# Nexa Blog Starter Pack

This is a starter pack for building a blog application using Next.js, featuring server-side rendering (SSR), static site generation (SSG), and React Query for data fetching. The project integrates with an external API for dynamic content management.

## GitHub Repository

[View Repository](https://github.com/Apollo-Level2-Web-Dev/nexa-blog-starter-pack)

## Table of Contents

1. [Project Setup](#project-setup)
2. [Features](#features)
3. [Getting Started](#getting-started)
4. [File Structure](#file-structure)
5. [Fetching Data](#fetching-data)
   - [Caching and Revalidating](#caching-and-revalidating)
   - [Server-Side Rendering](#server-side-rendering)
   - [Dynamic Data Retrieval](#dynamic-data-retrieval)
   - [Static Site Generation](#static-site-generation)
6. [Creating Blogs](#creating-blogs)
7. [Generating Metadata](#generating-metadata)
8. [API Route Handlers](#api-route-handlers)
9. [Using RTK Query](#using-rtk-query)
10. [License](#license)

## Project Setup

### Initial Project Setup

1. Clone the repository.
   ```bash
   git clone https://github.com/Apollo-Level2-Web-Dev/nexa-blog-starter-pack.git
   cd nexa-blog-starter-pack
   ```
2. Set up the external server (e.g., JSON server).
3. Install dependencies.
   ```bash
   npm install
   ```

## Features
- Fetch and display the latest blogs.
- Server-side rendering for dynamic content.
- Create new blog posts using Next.js form components.
- Generate metadata for SEO.
- Uses Redux Toolkit with RTK Query for managing state and data fetching.

## Getting Started

1. Run the development server.
   ```bash
   npm run dev
   ```
2. Access the application at [http://localhost:3000](http://localhost:3000).

## File Structure

```plaintext
src/
├── app/
│   ├── blogs/
│   │   ├── [blogId]/
│   │   │   ├── route.ts
│   │   │   └── page.tsx
│   │   ├── create/
│   │   └── page.tsx
│   ├── components/
│   │   ├── LatestBlogs/
│   │   ├── ui/
│   │   └── BlogCard.tsx
│   └── page.tsx
├── redux/
│   └── apis/
│       └── blogs.slice.ts
└── types/
    └── index.ts
```

## Fetching Data

### Caching and Revalidating

In `src/app/page.tsx`, fetch the latest blogs with revalidation enabled:

```typescript
const HomePage = async () => {
  const res = await fetch("http://localhost:5000/blogs", {
    next: {
      revalidate: 30,
    },
  });
  const blogs = await res.json();
  return (
    <div className="my-10">
      <LatestBlogs blogs={blogs} />
    </div>
  );
};
```

### Server-Side Rendering

Use SSR for displaying all blogs:

```typescript
const res = await fetch("http://localhost:5000/blogs", {
  cache: "no-store", // By default, happens
});
```

### Dynamic Data Retrieval

Retrieve dynamic data with an ID for the detail page:

```typescript
const BlogDetailsPage = async ({ params }) => {
  const { blogId } = await params;
  const res = await fetch(`http://localhost:5000/blogs/${blogId}`);
  const blog = await res.json();
  // ...
};
```

### Static Site Generation

Use `generateStaticParams()` for SSG:

```typescript
export const generateStaticParams = async () => {
  const res = await fetch(`http://localhost:5000/blogs`);
  const blogs = await res.json();
  return blogs.slice(0, 3).map(blog => ({ blogId: blog.id }));
};
```

## Creating Blogs

### Using Next.js Form Component

Refer to the [Next.js Form Documentation](https://nextjs.org/docs/app/api-reference/components/form) to create forms for new blogs.

### Using Next.js Server Actions

Create a new blog or perform mutations in `src/action/createBlog.ts`:

```typescript
"use server";

export const createBlog = async (data: FormData) => {
  const blogData = Object.fromEntries(data.entries());
  const res = await fetch("http://localhost:5000/blogs", {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
    },
    body: JSON.stringify(blogData),
  });
  const blogInfo = await res.json();
  if (blogInfo) {
    redirect(`/blogs/${blogInfo.id}`);
  }
  return blogInfo;
};
```

## Generating Metadata

Use `generateMetadata()`:

```typescript
export async function generateMetadata({ params }) {
  const { blogId } = await params;
  const res = await fetch(`http://localhost:5000/blogs/${blogId}`);
  const blog = await res.json();
  return {
    title: blog.title,
    description: blog.description,
  };
}
```

## API Route Handlers

Create an API route to handle GET requests in `src/app/blogs/[blogId]/route.ts`:

```typescript
import { NextResponse } from "next/server";

export const GET = async (request, { params }) => {
  const { id } = await params;
  const blog = blogs.find(blog => blog.id === id);
  return NextResponse.json(blog);
};
```

## Using RTK Query

### Client-Side Data Fetching

Set up RTK Query with Redux Toolkit for client-side data fetching.

```bash
npm install @reduxjs/toolkit react-redux
```

Here’s how to set up your client-side page using RTK Query:

```typescript
const BlogsPage = () => {
  const { data: blogs, isLoading } = useGetBlogsQuery({});
  if (isLoading) {
    return <Spinner />;
  }

  return (
    <div className="mx-auto">
      {/* Blog Display Logic */}
    </div>
  );
};
```

## License

This project is licensed under the MIT License.
```

### Notes:
- Modify sections as needed to fit your specific requirements or setup.
- Ensure you test the links and programmatically display data according to your specifications.

Let me know if you need further adjustments or additional information! 

# NexaBlog

## Installation:

1. Clone the repository.
2. Install dependencies using `npm install`.
3. Run the project using `npm run dev`.
