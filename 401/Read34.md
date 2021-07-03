# React IIII

## Dynamic Routes

### Statically Generate Pages with Dynamic Routes

To create dynamic routes, follow these steps:

* Create a page called [id].js, pages inside square brackets are dynamic routes.
* inside this page add that code that renders any page as usual.
* Exports an async function called `getStaticPaths` from this page, that returns a list of possible values for `id`.
* Implement `getStaticProps` function to fetch necessary data with a given `id`.

### Implement getStaticPaths

* Import and add a layout function inside the `[id].js` page.
* Open the original page and add a `getAllPostIds` function that will return the list of filenames(excluding `.md`)
* Import `getAllPostIds` function to the [id].js page.

### Implement getStaticProps

* Inside the original page, add getPostData function that returns the data based on `id`.
* Import the function `{ getAllPostIds }` to the [id].js page.
* Add the following code:

    ```js
    export async function getStaticProps({ params }) {
        const postData = getPostData(params.id)
        return {
            props: {
                postData
            }
        }
    }
    ```

* Update the component that renders the data, to use `PostData` as parameter.

## Deploy Next.js App

### Push the code into GitHub

### Deploy to Vercel

* Create Vercel account.
* Install Vercel for GitHub, and give it access on all repositories.
* Import Nextjs Repository using this link [import/git](https://vercel.com/import/git).
* Vercel automatically detects that you have a Next.js app and chooses optimal build settings for you.