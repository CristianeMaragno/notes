Next.js is a React framework for building full-stack web applications.
Next.js also abstracts and automatically configures tooling needed for React, like bundling, compiling, and more. This allows you to focus on building your application instead of spending time with configuration.

**Features**
Routing: A file-system based router built on top of Server Components that supports layouts, nested routing, loading states, error handling, and more.
- Next.js has two different routers: the App Router and the Pages Router. The App Router is a newer router. The Pages Router is still getting support.
- The file system organization is important because each folder in a route represents a route segment. Each route segment is mapped to a corresponding segment in a URL path.(App Router)
	![[tree.png|300]]
- The React components defined in special files of a route segment are rendered in a specific hierarchy: > layout.js > template.js > error.js (React error boundary) > loading.js (React suspense boundary > not-found.js (React error boundary) > page.js or nested layout.js(App Router)
- In Next.js, a page is a React Component exported from a .js, .jsx, .ts, or .tsx file in the pages directory. Each page is associated with a route based on its file name. For neseted page, you use the organization `pages/blog/first-post.js` → `/blog/first-post`
- Next.js supports pages with dynamic routes. For example, if you create a file called pages/posts/[id].js, then it will be accessible at posts/1, posts/2, etc.
- If you only have one layout for your entire application, you can create a Custom App and wrap your application with the layout. Since the <Layout /> component is re-used when changing pages, its component state will be preserved.
	```
	import Layout from '../components/layout' 
	export default function MyApp({ Component, pageProps }) { 
		return ( 
			<Layout> 
				<Component {...pageProps} /> 
			</Layout> 
		)
	}
	```

Rendering: Client-side and Server-side Rendering with Client and Server Components. Further optimized with Static and Dynamic Rendering on the server with Next.js. Streaming on Edge and Node.js runtimes.

Data Fetching:	Simplified data fetching with async/await in Server Components, and an extended fetch API for request memoization, data caching and revalidation.

Styling: Support for your preferred styling methods, including CSS Modules, Tailwind CSS, and CSS-in-JS

Optimizations: Image, Fonts, and Script Optimizations to improve your application's Core Web Vitals and User Experience.

TypeScript:	Improved support for TypeScript, with better type checking and more efficient compilation, as well as custom TypeScript Plugin and type checker.