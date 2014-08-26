#Rspec + Rails
### Get your rspec
you need to have a features file
```
rails generate rspec install
```
require capybara!

## example feature file for craigslist
```ruby
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
```
