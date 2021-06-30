# Next.js

## Create Next.js app

To start next.js app with tailwind CSS do the following

* Open terminal and type the following  

    ```bash
    yarn create next-app -e with-tailwind app-name "gitHub-link"
    ```

* Enter the directory

    `cd app-name`

* Run development server

    `yarn dev`

### Welcome to Next.js

You should see a page like this when you access `http://localhost:3000`. This is the starter template page which shows some helpful information about Next.js.

![welcome](https://nextjs.org/static/images/learn/create-nextjs-app/welcome-to-nextjs.png)

#### The changes should be on `index.js` file

## Assets, Metadata, and CSS

### Download Starter Code

`npx create-next-app app-name --use-npm --example "gitHub-link"`

### Assets

Next.js can serve static assets, like images, under the top-level public directory. Files inside public can be referenced from the root of the application similar to pages.

The public directory is also useful for robots.txt, Google Site Verification, and any other static assets.

#### Download Your Profile Picture

First, let's retrieve your profile picture.

* Download your profile picture in .jpg format.
* Create an images directory inside of the public directory.
* Save the picture as profile.jpg in the public/images directory.
* The image size can be around 400px by 400px.
* You may remove the unused SVG logo file directly under the public directory.

#### Unoptimized Image

With regular HTML, you would add your profile picture as follows:

`<img src="/images/profile.jpg" alt="Your Name" />`
However, this means you have to manually handle:

* Ensuring your image is responsive on different screen sizes
* Optimizing your images with a third-party tool or library
* Only loading images when they enter the viewport

And more. Instead, Next.js provides an Image component out of the box to handle this for you.

#### Image Component and Image Optimization

next/image is an extension of the HTML `<img>` element, evolved for the modern web.

Next.js also has support for Image Optimization by default. This allows for resizing, optimizing, and serving images in modern formats like **WebP** when the browser supports it. This avoids shipping large images to devices with a smaller viewport. It also allows Next.js to automatically adopt future image formats and serve them to browsers that support those formats.

Automatic Image Optimization works with any image source. Even if the image is hosted by an external data source, like a **CMS**, it can still be optimized.

#### Using the Image Component

```js
import Image from 'next/image'

const YourComponent = () => (
  <Image
    src="/images/profile.jpg" // Route of the image file
    height={144} // Desired size with correct aspect ratio
    width={144} // Desired size with correct aspect ratio
    alt="Your Name"
  />
)
```

### Metadata

`<title>` is part of the `<head>` HTML tag, so let's dive into how we can modify the `<head>` tag in a Next.js page.

Open pages/index.js in your editor and find the following lines:

```html
<Head>
  <title>Create Next App</title>
  <link rel="icon" href="/favicon.ico" />
</Head>
```

You can import the Head component from the 'next/head' module.

Adding Head to first-post.js

Open the pages/posts/first-post.js file and add an import for Head from next/head at the beginning of the file:

`import Head from 'next/head'`

Then, update the exported FirstPost component to include the Head component. For now, we‘ll add just the title tag:

```js
export default function FirstPost() {
  return (
    <>
      <Head>
        <title>First Post</title>
      </Head>
      <h1>First Post</h1>
      <h2>
        <Link href="/">
          <a>Back to home</a>
        </Link>
      </h2>
    </>
  )
}
```

### CSS Styling

As you can see, our index page `(http://localhost:3000)` already has some styles. If you take a look at pages/index.js, you should see code like this:

```js
<style jsx>{`
  …
`}</style>
```

This page is using a library called `styled-jsx`. It’s a “CSS-in-JS” library — it lets you write CSS within a React component, and the CSS styles will be scoped (other components won’t be affected).

Next.js has built-in support for styled-jsx, but you can also use other popular CSS-in-JS libraries such as styled-components or emotion.

#### Writing and Importing CSS

Next.js has built-in support for CSS and Sass which allows you to import .css and .scss files.

Using popular CSS libraries like Tailwind CSS is also supported.

#### Layout Component

First, Let’s create a Layout component which will be shared across all pages.

Create a top-level directory called `components`.
Inside components, create a file called `layout.js` with the following content:

```js
export default function Layout({ children }) {
  return <div>{children}</div>
}
```

Then, open `pages/posts/first-post.js`, add an import for the Layout component, and make it the outermost component:

```js
import Head from 'next/head'
import Link from 'next/link'
import Layout from '../../components/layout'

export default function FirstPost() {
  return (
    <Layout>
      <Head>
        <title>First Post</title>
      </Head>
      <h1>First Post</h1>
      <h2>
        <Link href="/">
          <a>Back to home</a>
        </Link>
      </h2>
    </Layout>
  )
}
```

#### Adding CSS

Now, let’s add some styles to the Layout component. To do so, we’ll use CSS Modules, which lets you import CSS files in a React component.

Create a file called components/layout.module.css with the following content:

```css
.container {
  max-width: 36rem;
  padding: 0 1rem;
  margin: 3rem auto 6rem;
}
``
Important: To use CSS Modules, the CSS file name must end with .module.css.

To use this container class inside components/layout.js, you need to:

* Import the CSS file and assign a name to it, like styles
* Use styles.container as the className

Open components/layout.js and replace its content with the following:

```js
import styles from './layout.module.css'

export default function Layout({ children }) {
  return <div className={styles.container}>{children}</div>
}
```

### Global Styles

CSS Modules are useful for component-level styles. But if you want some CSS to be loaded by every page, Next.js has support for that as well.

To load global CSS files, create a file called pages/_app.js with the following content:

```js
export default function App({ Component, pageProps }) {
  return <Component {...pageProps} />
}
```

This App component is the top-level component which will be common across all the different pages. You can use this App component to keep state when navigating between pages, for example.

Restart the Development Server
Important: You need to restart the development server when you add pages/_app.js. Press `Ctrl + c` to stop the server and run:

#### Adding Global CSS

In Next.js, you can add global CSS files by importing them from pages/_app.js. You cannot import global CSS anywhere else.

The reason that global CSS can't be imported outside of pages/_app.js is that global CSS affects all elements on the page.

If you were to navigate from the homepage to the /posts/first-post page, global styles from the homepage would affect /posts/first-post unintentionally.

You can place the global CSS file anywhere and use any name. So let’s do the following:

Create a top-level styles directory and create global.css inside.
Add the following content to styles/global.css. It resets some styles and changes the color of the a tag:

```html
html,
body {
  padding: 0;
  margin: 0;
  font-family: -apple-system, BlinkMacSystemFont, Segoe UI, Roboto, Oxygen, Ubuntu,
    Cantarell, Fira Sans, Droid Sans, Helvetica Neue, sans-serif;
  line-height: 1.6;
  font-size: 18px;
}
``
