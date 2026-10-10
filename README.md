# Tasteorama — Frontend

The React frontend of Tasteorama, a team recipe application. Visitors can browse recipes, search by name, filter by category or ingredient and open cooking instructions. Registered users can add recipes and manage their saved favourites.

[Live demo](https://tasteorama-tau.vercel.app/) · [Backend repository](https://github.com/Slavik756/Response-201-back)

## Features

- Recipe catalog with pagination and filtering.
- Recipe details with ingredients and cooking instructions.
- Registration, login and logout interfaces.
- Protected pages for adding a recipe and viewing a personal profile.
- Recipe creation with an image, ingredient measurements and form validation.
- Separate profile views for personal and saved recipes.
- Favourite controls, loading states, error messages and confirmation modals.
- Responsive navigation and page layouts.

## Stack

React 18, React Router 6, Redux Toolkit, React Redux, Redux Persist, Axios, Formik, Yup, CSS Modules and Vite 7.

## Run locally

Use Node.js 22.12 or later and npm.

```sh
git clone https://github.com/Slavik756/Response-201-Front.git
cd Response-201-Front
npm ci
npm run dev
```

Open the URL printed by Vite, normally [http://localhost:5173](http://localhost:5173).

| Command | Purpose |
| --- | --- |
| `npm run dev` | Start the development server |
| `npm run build` | Generate a production build in `dist/` |
| `npm run preview` | Preview the production build |
| `npm run lint` | Run ESLint |

## Backend connection

The current source points to:

```text
https://response-201-back.onrender.com/api
```

This URL is hard-coded in the authentication operations and several recipe-related modules. A `VITE_API_URL` environment variable is not currently implemented. The frontend does not need MongoDB or Cloudinary credentials.

To connect a locally running backend, replace the existing API URL with `http://localhost:3000/api` throughout `src/`, including both the Axios default URL and absolute request URLs. Follow the [backend setup instructions](https://github.com/Slavik756/Response-201-back#readme) for database and upload configuration.

The app sends the access token as an `Authorization: Bearer …` header. Its current-user restoration reads a saved token and requests `/user/current`; it does not implement automatic refresh-token rotation.

## Application routes

| Route | Screen |
| --- | --- |
| `/` | Recipe catalog, search and filters |
| `/register` | Registration |
| `/login` | Login |
| `/recipes/:recipeId` | Recipe details |
| `/add-recipe` | Add a recipe; authentication required |
| `/profile/own` | Personal recipes; authentication required |
| `/profile/favorites` | Saved recipes; authentication required |
| `/profile` | Redirect to personal recipes |
| Any other path | Not-found page |

## Structure

```text
src/
├── components/      # Forms, navigation, recipe cards, filters and modals
├── pages/           # Catalog, authentication, recipe and profile screens
├── redux/
│   ├── auth/        # Authentication state and requests
│   ├── recipes/     # Recipe state and requests
│   ├── filters/     # Filter state
│   └── store.js     # Redux store and persistence
├── main.jsx         # React entry point and providers
└── index.css        # Shared styles
vite.config.js
vercel.json          # SPA route fallback
```

## Implementation notes

Category and ingredient filters are sent to the API. Name search currently fetches up to 500 recipes and filters them in the browser.

The frontend and backend are separate deployments. Catalog data, authentication and saved recipes depend on the API being available. The repository includes a Vercel rewrite so direct visits to client-side routes load the application.

Tasteorama is a team project. This README describes the frontend's responsibilities; server routes, database models and upload handling are documented in the backend repository.
