# Dr Squatch Frontend Takehome

## Recommended IDE Setup

[VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and disable Vetur) + [TypeScript Vue Plugin (Volar)](https://marketplace.visualstudio.com/items?itemName=Vue.vscode-typescript-vue-plugin).

## JavaScript Framework Used
Project created by using `npm init vue@latest` (Vue.js + Vite)

## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Compile and Minify for Production

```sh
npm run build
```

## Project Requirements 
```sh
- Create a wireframe using api from Base URL: https://ae3t7l1i79.execute-api.us-east-1.amazonaws.com/
- Utiltize endpoints: GET /bundles, GET /product/{handle}
- Project Requirements 
    - Display the following information for a bundle: image, title, price, original price (if applicable), scent profile, and included products.
    - The scent filter should be at the top of the page, with available scent options listed. It may be a group of checkboxes, a drop down, or any other UI format you want. The filter must be functional; the options selected updates the bundles displayed.
    - (Optional) Make the page responsive.
    - (Optional) Use the scent specific colors: woodsy: #165834, citrus: #de7c00, fresh: #006fd6, herbal: #5a3714, rich: #e0a17e, spiced: #c10000
- Should have reuseable components
- Files / Folder Structure
    app/
    - src/
        - components/
        -- Card.vue
    - App.vue
- Layout should be responsive
    - Phones and Tablets to have one column
    - Desktops should have two columns
```
