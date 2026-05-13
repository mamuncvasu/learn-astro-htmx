# Astro Minimum Learning [static site builder and api integration] -- not yet completed

    Target : সিভাসু ওয়েবসাইটকে static আকারে তৈরী করা, 
    যেখানে Api কল করে node adaptor diye Rails-backend থেকে data আনবো। 
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

## Server Rendering [https://docs.astro.build/en/guides/on-demand-rendering/] -- ok (very important)

		Prerequisites : run with Adapter [node]

			npx astro add node
			npm run build
			node ./dist/server/entry.mjs
			HOST=0.0.0.0 PORT=4321 node ./dist/server/entry.mjs 

		way 01 : any specific page (src/page/post.astro) using "export const prerender = false;"
		---
		export const prerender = false;
		const response = await fetch('http://localhost:3000/posts.json');
		const posts = await response.json();
		---
		<h1> All Blog Posts</h1>
		    {posts.map(post => (
		    <article>
		        <h2>{post.title}</h2>
		        <p>{post.body}</p>
		    </article>
		    ))}

		Way 02 : all site using config file () using output: 'server', but cab be avoid in a page using "export const prerender = true;"

		import { defineConfig } from 'astro/config';
		import node from '@astrojs/node';
		export default defineConfig({
		  output: 'server',
		  adapter: node({
		    mode: 'standalone'
		  })
		});

## Api call and Data integration [Rails 8 api + Astro Frontend]  --- problem: শুধু ডেভেলপমেন্টে কাজ করে , build করে ফেললে শুধু static কনটেন্ট দেখায়। 

    Step 01: rails app

        rails new api-backend
        cd api-backend
        rails g scaffold Post title body:text
        rails db:migrate
        bundle add faker rack-cors
        edit: seed.rb
            1000.times  do
	            Post.create(
                title: Faker::Lorem.sentence ,
                body: Faker::Lorem.paragraph
                )
            end

        rails db:seed
        edit: config/initializers/cors.rb
	        Rails.application.config.middleware.insert_before 0, Rack::Cors do
			  allow do
			    origins '*'
			    resource '*', headers: :any, methods: [:get, :post, :patch, :put]
			  end
			end
			
		rails s
        localhost:3000/posts.json

    Step 02: Astro Frontend

        create a page: "page/post"

        ---
        const response = await fetch('http://localhost:3000/posts.json');
        const posts = await response.json();
        ---
        <h1> All Blog Posts</h1>
            {posts.map(post => (
            <article>
                <h2>{post.title}</h2>
                <p>{post.body}</p>
            </article>
            ))}

        Now Browse : localhost:4321/post

## Build, Preview and Deploy

    npm run build
    npm run preview

## Https on build site

	SERVER_KEY_PATH=./private/key.pem SERVER_CERT_PATH=./private/cert.pem node ./dist/server/entry.mjs
	
## Advanced : authentication and authorization [https://docs.astro.build/en/guides/authentication/]



## Advanced : Astro with SolidJs [https://docs.astro.build/en/guides/integrations-guide/solid-js/]

	1) npx astro add solid
	2) create (src/components/MySolidComponent.jsx) and write solidjs code:
		
		function CharacterName() {
		  const [name] = createResource(() =>
		    fetch('https://swapi.dev/api/people/1')
		      .then((result) => result.json())
		      .then((data) => data.name)
		  );
		
		  return (
		    <>
		      <h2>Name:</h2>
		      {/* Luke Skywalker */}
		      <div>{name()}</div>
		    </>
		  );
		}
	
	3) use that component in a page ()

		---
		import MyReactComponent from '../components/MySolidComponent.jsx';
		---
		<html>
		  <body>
		    <h1>Use React components directly in Astro!</h1>
		    <MySolidComponent />
		  </body>
		</html>

## Advanced : Astro with React
