# htmx learning

## Static site with ruby 	
	- gem install webrick
	- mkdir htmx-practice & cd htmx-practice
	- ruby -run -e httpd . -p 8888

## Static site with nginx [ folder location :  /home/cvasu/htmx-practice] -- not ok yet
	
    server {
        listen       80;
        server_name  cvasu.dev;

        location / {
            root   /home/cvasu/htmx-practice;
            index  index.html index.htm;
        }
    }


## Backend Setup
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
        localhost:3000/posts

## htmx .html page -- not ok yet

	<article>
	    <div
	        hx-get="http://localhost:3000/posts"
	        hx-select="#posts"
	        hx-trigger="load 1s"
	        hx-swap="outerHTML"
	        hx-target="#results"
	    >
	        Loading...
	    </div>
	     <div id="results"></div>
	</article>
