#Rspec + Rails
### Get your rspec
You need to have a features file
```
rails generate rspec install
```
Don't forget to require capybara!

## Feature Tests
###Example feature testing for Craigslist
```ruby
require 'spec_helper'

feature 'Browsing categories' do
	let!(:category){Category.create!(name: 'Fake Category')}
	#show categories

	scenario 'shows categories' do
		visit(root_path)
		expect(page).to have_link('Fake Category')
	end

	#navigate categories
	scenario 'navigates categories' do
		category.articles.create(title: 'Fake Article', price:100)
		visit(root_path)
		click_link('Fake Category')
		expect(page).to have_content('Fake Category')
		expect(page).to have_link('Fake Article -$1.0')
	end

	#show an article
	scenario 'see article details' do
		article = cateogry.articles.create(title: 'Fake ARticle', price: 100)
		visit(category_path(category))
		click_link('Fake Article - $1.0')
		expect(page).to have_content(price -$1.0)
	end
end
```
*Note that a lot of things are happening here becuase it is integrated testing. These tests are using the database. They parse the whole HTML file. They are also testing all the behaviors. Integration tests are made of multiple interactions to produce a result.

*You only want to do things in the tests that users would concievably do. There should be no mocks or stubs.

## Controller Specs
Isolated unit test of controller behavior. Controllers are responsible for handling requests and then constructing a response. This is where you would stub and mock.
### Example

The following is not currently checking content. It is only checking if 200 goes through
```ruby
describe PostsController do
	describe "#index" do
		it "responds with a 200" do
			get :index
			expect(response.status).to eq 200
		end
	end
end
```
The following should pass
```ruby
describe CategoriesController do
	it 'renders the index view' do
		get :index
		expect(response.status).to eq(200)
	end
end
```
test data! Do you actually need to have an active record model to make this test run? No! Use a stub. You stub all the categories because yo want to ensure that tests run as quickly as possible. Without stubbing, you would end up writing to the db. This stub says that category will always return the array ``` [category] ```
```ruby
describe CategoriesController do
	it 'renders categories as json' do
		category = Category.new(name:'Fake Category')
		Category.stub(:all => [category])
		get :index, :format => :json
		body = JSON.parse(response.body)
		expect(body.length).to eq(1)
	end
end
```
### test a redirect

```ruby
	it 'redirects to rooth path' do
		get :show, :id =>1
		expect(page).to redirect_to('root_path')
	end
```

### test a create
note: you are allowed to have trailing commas in ruby. but not js
``` ruby
	describe articlesController do
		it 'creates a controller' do
			article_attributes = {
			title: 'Fake Article',
			price: '$1.59',
			}
		end
		# this line says please create a post request and post it to create
		# also could be article_path instead of :create
		post(:create, :article => article_attributes, :format => :json)
		body :JSON.partse(response.body)
		expect(body['title']).to eq 'Fake Article'
		expect(body['price']).to eq 159
	end
```