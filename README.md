# <img width="391" alt="image" src="https://github.com/user-attachments/assets/0e28a94a-2f45-4237-97aa-fbda95d07504">


# Overview
[KVision](https://kvision.io) codebase containing real world examples (CRUD, auth, advanced patterns, etc) that adheres to the [RealWorld](https://github.com/gothinkster/realworld) spec and API.

[Live Demo](https://centelha-hackathon-234ada9968a7.herokuapp.com/)

# Features
**Conduit** is a social blogging site (i.e. a Medium.com clone). It uses a custom API for all requests, including authentication.

- Authenticate users via JWT (login/signup pages + logout button on settings page)
- CRU- users (sign up & settings page - no deleting required)
- CRUD Articles
- CR-D Comments on articles (no updating required)
- GET and display paginated lists of articles
- Favorite articles
- Follow other users

## Requirements
### Header
#### Unauthenticated user
If no user is logged in, then the header should include links to:

- the home page
- the login page
- the register page
the link of the active page should use the **active** css class.

#### Authenticated user
If a user is logged in, then the header should include links to:

- the home page
- the new article page
- the settings page
- the profile page
the link of the active page should use the **active** css class.

### Pages
- Home page (URL: /#/ )
  - List of tags
  - List of articles pulled from either Feed, Global (default), or by Tag
  - Pagination for list of articles
  - an optional tag name tab, appears after clicking one of the popular tags
  - an optional Your Feed tab, appears after logging in
- Sign in/Sign up pages (URL: /#/login, /#/register )
  - Uses JWT (store the token in localStorage)
  - Authentication can be easily switched to session/cookie based
- Settings page (URL: /#/settings )
- Editor page to create/edit articles (URL: /#/editor, /#/editor/article-slug-here )
- Article page (URL: /#/article/article-slug-here )
  - Delete article button (only shown to article’s author)
  - Render markdown from server client side
  - Comments section at bottom of page
  - Delete comment button (only shown to comment’s author)
- Profile page (URL: /#/profile/:username , /#/profile/:username /favorites )
  - Show basic user info
  - List of articles populated from author’s created articles or author’s favorited articles

### Data Visibility
The visibility of user content is limited as follows:
- logged out users see only content created by demo accounts
- logged in users see only their content and the content created by demo accounts

# Development and Deployment

The frontend part is based on the [frontend only application](https://github.com/rjaros/kvision-realworld-example-app), created with [KVision](https://kvision.io) and written in pure Kotlin/JS.

This fullstack version is using [KVision server side interfaces](https://kvision.gitbook.io/kvision-guide/part-3-server-side-interface) with Spring Boot backend. It's based on Kotlin multiplatform architecture, with the common code
shared between the frontend and the backend side, and automatically generated JSON-RPC endpoints. 

The backend application is heavily based on [Kotlin coroutines](https://github.com/Kotlin/kotlinx.coroutines), 
utilizing Spring Webflux and R2DBC fully asynchronous and non-blocking services and interfaces.

The project is using in-memory H2 database during development and PostgreSQL when deployed to Heroku.

## Getting started

Make sure you have [JDK 8](https://openjdk.java.net/) or higher installed. Check other requirements of KVision [here](https://kvision.gitbook.io/kvision-guide/1.-getting-started-1/setting-up).

The project is build with Gradle Wrapper. Run Gradle build with `./gradlew` or `gradlew.bat` command.

### Running
Run in two separate terminals:
* `./gradlew backendRun` - Starts Spring Boot backend server on port 8080. 
* `./gradlew -t frontendRun` - Starts a webpack dev server on port 3000. 

Open http://localhost:3000 in a browser to work with both servers.

### Packaging
* `./gradlew jar` - Packages a fat jar archive with all required files into `build/libs/*.jar`. 

Run with `java -jar kvision-realworld-example-app-fullstack-1.0.0-SNAPSHOT.jar` command.

### Testing

* `./gradlew frontendTest` - Run frontend unit tests defined in `src/frontendTest/kotlin` source files. Test reports are generated into `build/reports/tests/frontendTest`.

### Deploying to Heroku

* See `Procfile` for an example of converting JDBC url to R2DBC url.
