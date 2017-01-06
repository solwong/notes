# Ruby style

## Common

- Align function parameters either all on the same line or one per line

```ruby
# bad
def self.create_translation(phrase_id, phrase_key, target_locale,
                            value, user_id, do_xss_check, allow_verification)
  ...
end

# good
def self.create_translation(phrase_id,
                            phrase_key,
                            target_locale,
                            value,
                            user_id,
                            do_xss_check,
                            allow_verification)
  ...
end

# good
def self.create_translation(
  phrase_id,
  phrase_key,
  target_locale,
  value,
  user_id,
  do_xss_check,
  allow_verification
)
  ...
end
```

- Do not use default arguments. Use an options hash instead
 
```ruby
# bad
def obliterate(things, gently = true, except = [], at = Time.now)
  ...
end

# good
def obliterate(things, options = {})
  default_options = {
    :gently => true, # obliterate with soft-delete
    :except => [], # skip obliterating these things
    :at => Time.now, # don't obliterate them until later
  }
  options.reverse_merge!(default_options)

  ...
end
```

- Avoid class << self except when necessary, e.g. single accessors and aliased attributes

```ruby
class TestClass
  # bad
  class << self
    def first_method
      ...
    end

    def second_method_etc
      ...
    end
  end

  # good
  class << self
    attr_accessor :per_page
    alias_method :nwo, :find_by_name_with_owner
  end

  def self.first_method
    ...
  end

  def self.second_method_etc
    ...
  end
end
```

- Indent the public, protected, and private methods as much the method definitions they apply to. Leave one blank line above and below them

```ruby
class SomeClass
  def public_method
    # ...
  end

  private

  def private_method
    # ...
  end
end
```

- Don't use exceptions for flow of control

```ruby
# bad
begin
  n / d
rescue ZeroDivisionError
  puts "Cannot divide by 0!"
end

# good
if d.zero?
  puts "Cannot divide by 0!"
else
  n / d
end
```

- Avoid rescuing the Exception class

```ruby
# bad
begin
  # an exception occurs here
rescue Exception
  # exception handling
end

# good
begin
  # an exception occurs here
rescue StandardError
  # exception handling
end

# acceptable
begin
  # an exception occurs here
rescue
  # exception handling
end
```

- Don't specify RuntimeError explicitly in the two argument version of raise. Prefer error sub-classes for clarity and explicit error creation

```ruby
# bad
raise RuntimeError, 'message'

# better - RuntimeError is implicit here
raise 'message'

# best
class MyExplicitError < RuntimeError; end
raise MyExplicitError
```

- Collections

- Prefer map over collect.

- Prefer detect over find. The use of find is ambiguous with regard to ActiveRecord's find method - detect makes clear that you're working with a Ruby collection, not an AR object. 

- Prefer reduce over inject. 

- Prefer size over either length or count for performance reasons

- Be careful with ^ and $ as they match start/end of line, not string endings. If you want to match the whole string use: \A and \z

```ruby
string = "some injection\nusername"
string[/^username$/]   # matches
string[/\Ausername\z/] # don't match
```

- Use x modifier for complex regexps. This makes them more readable and you can add some useful comments. Just be careful as spaces are ignored

```ruby
regexp = %r{
  start         # some text
  \s            # white space char
  (group)       # first group
  (?:alt1|alt2) # some alternation
  end
}x
```

- Prefer parentheses over curly braces, brackets, or pipes when using %-literal delimiters for consistency, and because the behavior of %-literals is closer to method calls than the alternatives

```ruby
# bad
%w[date locale]
%w{date locale}
%w|date locale|

# good
%w(date locale)
```

## Percent Literals

- Prefer parentheses over curly braces, brackets, or pipes when using %-literal delimiters for consistency, and because the behavior of %-literals is closer to method calls than the alternatives

```ruby
# bad
%w[date locale]
%w{date locale}
%w|date locale|

# good
%w(date locale)
```

- Use %() for single-line strings which require both interpolation and embedded double-quotes. For multi-line strings, prefer heredocs

```ruby
# bad - no interpolation needed
%(<div class="text">Some text</div>)
# should be '<div class="text">Some text</div>'

# bad - no double-quotes
%(This is #{quality} style)
# should be "This is #{quality} style"

# bad - multiple lines
%(<div>\n<span class="big">#{exclamation}</span>\n</div>)
# should be a heredoc.

# good - requires interpolation, has quotes, single line
%(<tr><td class="name">#{name}</td>)```

### Use %r only for regular expressions matching more than one '/' character

```ruby
# bad
%r(\s+)

# still bad
%r(^/(.*)$)
# should be /^\/(.*)$/

# good
%r(^/blog/2011/(.*)$)```

### Avoid the use of %x unless you're going to invoke a command with backquotes in it (which is rather unlikely)

```ruby
# bad
date = %x(date)

# good
date = `date`
echo = %x(echo `date`)
```

## Rails

- When immediately returning after calling render or redirect_to, put return on the next line, not the same line

```ruby
# bad
render :text => 'Howdy' and return

# good
render :text => 'Howdy'
return

# still bad
render :text => 'Howdy' and return if foo.present?

# good
if foo.present?
  render :text => 'Howdy'
  return
end
```


