# TDD: test driven development
	ensures that there is no untested code
## TDD cycle
	Red Green Refactor
	+ see code fail
	+ see code pass
	+ refactor


## first test	
```ruby
	attr_reader :type
	class Cookie
		def initialize (type)
		@type = type
	end

```

```ruby
describe Cookie do
	it 'has a type' do
		cookie = Cookie.new('peanut butter')
		expect(cookie.type).to eq ('peanut butter')
	end
end
```

## second test
```ruby
	attr_reader :type, :time_baked
	class Cookie
		def initialize (type)
		@type = type
		@time_baked = 0
	end

```
``` ruby
	it 'has a type' do
		cookie = Cookie.new('peanut butter')
		expect(cookie.type).to eq ('peanut butter')
	end
	it 'has a baking time' do
		cookie = Cookie.new('peanut butter')
		expect(cookie.time_baked).to be_zero
	end
end
```
Refactor! we assign cookie twice, so we should do stuff.
``` ruby
	it 'has a type' do
		cookie = Cookie.new('peanut butter')
		expect(cookie.type).to eq ('peanut butter')
	end
	it 'has a baking time' do
		cookie = Cookie.new('peanut butter')
		expect(cookie.time_baked).to be_zero
		cookie.time_baked.zero?
	end
end
```
