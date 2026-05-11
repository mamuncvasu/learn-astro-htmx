# Astro Minimum Learning [static site builder and api integration] -- not yet completed

    Target : সিভাসু ওয়েবসাইটকে static আকারে তৈরী করা, 
    যেখানে Api কল করে Rails-backend থেকে data আনবো। 
    jekyll+Htmx এর চেয়ে ভালো নাকি দেখবো ?

## Install and run astro [https://docs.astro.build/en/install-and-setup/]

    npm create astro@latest 
    npm create astro@latest -- --add react --add partytown
    
    npm install
    npm run dev

## Astro with template [https://github.com/withastro/astro/tree/main/examples]
    
    npm create astro@latest -- --template with-tailwindcss
  

## Add TailwindCSS in Existing site -- ok

    1. npx astro add tailwind
    2. Import to layout "src/layouts/Layout.astro" and add frontmatter:
        ---
        import "../styles/global.css";
        ---

## Astro and tailwind new project [https://tailwindcss.com/docs/installation/framework-guides/astro] -- not tried

## Layout and Frontmatter

## Components

    1. create "components/FooterBase.astro"
    2. Use it in a layout or Page :
         ---
         import Footer from '../components/FooterBase.astro';
         ---
         <FooterBase />

## Astro.props

## Api call and Data integration

## Build, Preview and Deploy

    npm run build
    npm run preview

## Advanced : Astro with SolidJs

## Advanced : Astro with React
