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
	def baked!(time)
		@time_baked = time
	end
end
```

But what if we bake a little more?

``` ruby
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
```
The smallest amount of code changes what is happening!
```ruby

class Cookie
	attr_reader :type, :time_baked
	def initialize (type)
		@type = type
		@time_baked = 0
	end
	def baked!(time)
		@time_baked += time
	end
end

```
## Test number 4

```ruby
	describe 'cookie status' do
		it 'should have a status' do
			cookie.bake!(4)
			expect(cookie.status).to eq(:undercooked)
		end
	end
```
So we wrote the smallest amount of code...but is it really effective?
```ruby
class Cookie
	attr_reader :type, :time_baked
	def initialize (type)
		@type = type
		@time_baked = 0

	end
	def baked!(time)
		@time_baked += time
	end

	def status 
		@undercooked
	end
end
```

test again

```ruby
	describe 'cookie status' do
		it 'should have be undercookied' do
			cookie.bake!(4)
			expect(cookie.status).to eq(:undercooked)
		end
		it 'should tell me that it is properly cooked' do
			cookie.bake!(7)
			expect(cookie.status).to eq(:perfect)
		end
	end
```
 but woah. 7 minute cookies are undercooked. so rewrite
```ruby
class Cookie
	attr_reader :type, :time_baked
	def initialize (type)
		@type = type
		@time_baked = 0

	end
	def baked!(time)
		@time_baked += time
	end

	def status
		if time_baked<7
			:undercooked
		else
			:perfect
		end
	end
end
```

can we burn cookies?
```ruby
describe 'cookie status' do
	it 'should have be undercookied' do
		cookie.bake!(4)
		expect(cookie.status).to eq(:undercooked)
	end
	it 'should tell me that it is properly cooked' do
		cookie.bake!(7)
		expect(cookie.status).to eq(:perfect)
	end
	it 'should tell me that it is burned' do
		cookie.bake!(20)
		expect(cookie.status).to eq(:burned)
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
	def baked!(time)
		@time_baked += time
	end

	def status
		if @time_baked<7
			:undercooked
		elseif @time_baked > 12
			:burned
		else
			:perfect
		end
	end
end
```
woah woah it broke.

```ruby
describe 'cookie status' do
	it 'should have be undercookied' do
		cookie.bake!(4)
		expect(cookie.status).to eq(:undercooked)
	end
	it 'should tell me that it is properly cooked' do
		cookie.bake!(10)
		expect(cookie.status).to eq(:perfect)
	end
	it 'should tell me that it is burned' do
		cookie.bake!(20)
		expect(cookie.status).to eq(:burned)
	end

	it 'should tell me that it is chewy' do
		cookie.bake!(7)
		expect(cookie.status).to eq(:chewy)
	end
end
```
Refactor!!!
``` ruby
	def status
		if @time_baked<7
			:undercooked
		elseif @time_baked <10
			:chewy
		elseif @time_baked<12
			:perfect
		else
			:burned
		end
	end
```