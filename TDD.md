# TDD: test driven development
Ensures that there is no untested code
## TDD cycle
Red Green Refactor
+ see code fail
+ see code pass
+ refactor


## first test	
```ruby
	class Cookie
		attr_reader :type, :time_baked
		def initialize (type)
			@type = type
		end
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
	
	class Cookie
		attr_reader :type, :time_baked
		def initialize (type)
			@type = type
			@time_baked = 0
		end
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
let (:cookie){Cookie.new('peanut butter')}
	it 'has a type' do
		expect(cookie.type).to eq ('peanut butter')
	end
	it 'has a baking time' do
		expect(cookie.time_baked).to eq(0)
	end
end
```

## 3rd time!


``` ruby
let (:cookie){Cookie.new('peanut butter')}
	it 'has a type' do
		expect(cookie.type).to eq ('peanut butter')
	end
	it 'has a baking time' do
		expect(cookie.time_baked).to eq(0)
	end

	describe 'baking' do
		it 'should bake cookie a litle' do
			cookie.bake!(4)
			expect(cookie.time_baked).to eq(4)
		end
	end
end
```


```ruby
	
	class Cookie
		attr_reader :type, :time_baked
		def initialize (type)
			@type = type
			@time_baked = 0
		end
	end

	def baked!(time)
		@time_baked = time
	end

```

But what if we bake a little more?

``` ruby
let (:cookie){Cookie.new('peanut butter')}
	it 'has a type' do
		expect(cookie.type).to eq ('peanut butter')
	end
	it 'has a baking time' do
		expect(cookie.time_baked).to eq(0)
	end

	describe 'baking' do
		it 'should bake cookie a litle' do
			cookie.bake!(4)
			expect(cookie.time_baked).to eq(4)
		end
		it 'should bake cookie a lot' do
			cookie.bake!(4)
			cookie.bake!(2)
			expect(cookie.time_baked).to eq(6)
		end
	end
end
```
The smallest amount of code changes what is happening!
```ruby
	
	class Cookie
		attr_reader :type, :time_baked
		def initialize (type)
			@type = type
			@time_baked = 0
		end
	end

	def baked!(time)
		@time_baked += time
	end

```
