# Source Code Layout
> Nearly everybody is convinced that every style but their own is
> ugly and unreadable. Leave out the "but their own" and they're
> probably right... <br>
> -- Jerry Coffin (on indentation)

* <a name="utf-8"></a>
  Use `UTF-8` as the source file encoding.
<sup>[[link](#utf-8)]</sup>

* <a name="spaces-indentation"></a>
  Use two **spaces** per indentation level (aka soft tabs). No hard tabs.
<sup>[[link](#spaces-indentation)]</sup>

  ```Ruby
  # bad - four spaces
  def some_method
      do_something
  end

  # good
  def some_method
    do_something
  end
  ```

* <a name="crlf"></a>
  Use Unix-style line endings. (*BSD/Solaris/Linux/OS X users are covered by
  default, Windows users have to be extra careful.)
<sup>[[link](#crlf)]</sup>

  * If you're using Git you might want to add the following
    configuration setting to protect your project from Windows line
    endings creeping in:

    ```bash
    $ git config --global core.autocrlf true
    ```

* <a name="no-semicolon"></a>
  Don't use `;` to separate statements and expressions. As a corollary - use one
  expression per line.
<sup>[[link](#no-semicolon)]</sup>

  ```Ruby
  # bad
  puts 'foobar'; # superfluous semicolon

  puts 'foo'; puts 'bar' # two expressions on the same line

  # good
  puts 'foobar'

  puts 'foo'
  puts 'bar'

  puts 'foo', 'bar' # this applies to puts in particular
  ```

* <a name="single-line-classes"></a>
  Prefer a single-line format for class definitions with no body.
<sup>[[link](#single-line-classes)]</sup>

  ```Ruby
  # bad
  class FooError < StandardError
  end

  # okish
  class FooError < StandardError; end

  # good
  FooError = Class.new(StandardError)
  ```

* <a name="no-single-line-methods"></a>
  Avoid single-line methods. Although they are somewhat popular in the wild,
  there are a few peculiarities about their definition syntax that make their
  use undesirable. At any rate - there should be no more than one expression in
  a single-line method.
<sup>[[link](#no-single-line-methods)]</sup>

  ```Ruby
  # bad
  def too_much; something; something_else; end

  # okish - notice that the first ; is required
  def no_braces_method; body end

  # okish - notice that the second ; is optional
  def no_braces_method; body; end

  # okish - valid syntax, but no ; makes it kind of hard to read
  def some_method() body end

  # good
  def some_method
    body
  end
  ```

  One exception to the rule are empty-body methods.

  ```Ruby
  # good
  def no_op; end
  ```

* <a name="spaces-operators"></a>
  Use spaces around operators, after commas, colons and semicolons, around `{`
  and before `}`. Whitespace might be (mostly) irrelevant to the Ruby
  interpreter, but its proper use is the key to writing easily readable code.
<sup>[[link](#spaces-operators)]</sup>

  ```Ruby
  sum = 1 + 2
  a, b = 1, 2
  [1, 2, 3].each { |e| puts e }
  class FooError < StandardError; end
  ```

  The only exception, regarding operators, is the exponent operator:

  ```Ruby
  # bad
  e = M * c ** 2

  # good
  e = M * c**2
  ```

  `{` and `}` deserve a bit of clarification, since they are used
  for block and hash literals, as well as string interpolation.
  For hash literals two styles are considered acceptable.

  ```Ruby
  # good - space after { and before }
  { one: 1, two: 2 }

  # good - no space after { and before }
  {one: 1, two: 2}
  ```

  The first variant is slightly more readable (and arguably more
  popular in the Ruby community in general). The second variant has
  the advantage of adding visual difference between block and hash
  literals. Whichever one you pick - apply it consistently.

* <a name="no-spaces-braces"></a>
  No spaces after `(`, `[` or before `]`, `)`.
<sup>[[link](#no-spaces-braces)]</sup>

  ```Ruby
  some(arg).other
  [1, 2, 3].size
  ```

* <a name="no-space-bang"></a>
  No space after `!`.
<sup>[[link](#no-space-bang)]</sup>

  ```Ruby
  # bad
  ! something

  # good
  !something
  ```

* <a name="no-space-inside-range-literals"></a>
  No space inside range literals.
<sup>[[link](#no-space-inside-range-literals)]</sup>

    ```Ruby
    # bad
    1 .. 3
    'a' ... 'z'

    # good
    1..3
    'a'...'z'
    ```

* <a name="indent-when-to-case"></a>
  Indent `when` as deep as `case`. I know that many would disagree
  with this one, but it's the style established in both "The Ruby
  Programming Language" and "Programming Ruby".
<sup>[[link](#indent-when-to-case)]</sup>

  ```Ruby
  # bad
  case
    when song.name == 'Misty'
      puts 'Not again!'
    when song.duration > 120
      puts 'Too long!'
    when Time.now.hour > 21
      puts "It's too late"
    else
      song.play
  end

  # good
  case
  when song.name == 'Misty'
    puts 'Not again!'
  when song.duration > 120
    puts 'Too long!'
  when Time.now.hour > 21
    puts "It's too late"
  else
    song.play
  end
  ```

* <a name="indent-conditional-assignment"></a>
  When assigning the result of a conditional expression to a variable,
  preserve the usual alignment of its branches.
<sup>[[link](#indent-conditional-assignment)]</sup>

  ```Ruby
  # bad - pretty convoluted
  kind = case year
  when 1850..1889 then 'Blues'
  when 1890..1909 then 'Ragtime'
  when 1910..1929 then 'New Orleans Jazz'
  when 1930..1939 then 'Swing'
  when 1940..1950 then 'Bebop'
  else 'Jazz'
  end

  result = if some_cond
    calc_something
  else
    calc_something_else
  end

  # good - it's apparent what's going on
  kind = case year
         when 1850..1889 then 'Blues'
         when 1890..1909 then 'Ragtime'
         when 1910..1929 then 'New Orleans Jazz'
         when 1930..1939 then 'Swing'
         when 1940..1950 then 'Bebop'
         else 'Jazz'
         end

  result = if some_cond
             calc_something
           else
             calc_something_else
           end

  # good (and a bit more width efficient)
  kind =
    case year
    when 1850..1889 then 'Blues'
    when 1890..1909 then 'Ragtime'
    when 1910..1929 then 'New Orleans Jazz'
    when 1930..1939 then 'Swing'
    when 1940..1950 then 'Bebop'
    else 'Jazz'
    end

  result =
    if some_cond
      calc_something
    else
      calc_something_else
    end
  ```

* <a name="empty-lines-between-methods"></a>
  Use empty lines between method definitions and also to break up a method
  into logical paragraphs internally.
<sup>[[link](#empty-lines-between-methods)]</sup>

  ```Ruby
  def some_method
    data = initialize(options)

    data.manipulate!

    data.result
  end

  def some_method
    result
  end
  ```

* <a name="no-trailing-params-comma"></a>
  Avoid comma after the last parameter in a method call, especially when the
  parameters are not on separate lines.
<sup>[[link](#no-trailing-params-comma)]</sup>

  ```Ruby
  # bad - easier to move/add/remove parameters, but still not preferred
  some_method(
               size,
               count,
               color,
             )

  # bad
  some_method(size, count, color, )

  # good
  some_method(size, count, color)
  ```

* <a name="spaces-around-equals"></a>
  Use spaces around the `=` operator when assigning default values to method
  parameters:
<sup>[[link](#spaces-around-equals)]</sup>

  ```Ruby
  # bad
  def some_method(arg1=:default, arg2=nil, arg3=[])
    # do something...
  end

  # good
  def some_method(arg1 = :default, arg2 = nil, arg3 = [])
    # do something...
  end
  ```

  While several Ruby books suggest the first style, the second is much more
  prominent in practice (and arguably a bit more readable).

* <a name="no-trailing-backslash"></a>
  Avoid line continuation `\` where not required. In practice, avoid using
  line continuations for anything but string concatenation.
<sup>[[link](#no-trailing-backslash)]</sup>

  ```Ruby
  # bad
  result = 1 - \
           2

  # good (but still ugly as hell)
  result = 1 \
           - 2

  long_string = 'First part of the long string' \
                ' and second part of the long string'
  ```

* <a name="consistent-multi-line-chains"></a>
    Adopt a consistent multi-line method chaining style. There are two
    popular styles in the Ruby community, both of which are considered
    good - leading `.` (Option A) and trailing `.` (Option B).
<sup>[[link](#consistent-multi-line-chains)]</sup>

  * **(Option A)** When continuing a chained method invocation on
    another line keep the `.` on the second line.

    ```Ruby
    # bad - need to consult first line to understand second line
    one.two.three.
      four

    # good - it's immediately clear what's going on the second line
    one.two.three
      .four
    ```

  * **(Option B)** When continuing a chained method invocation on another line,
    include the `.` on the first line to indicate that the
    expression continues.

    ```Ruby
    # bad - need to read ahead to the second line to know that the chain continues
    one.two.three
      .four

    # good - it's immediately clear that the expression continues beyond the first line
    one.two.three.
      four
    ```

  A discussion on the merits of both alternative styles can be found
  [here](https://github.com/bbatsov/ruby-style-guide/pull/176).

* <a name="no-double-indent"></a>
    Align the parameters of a method call if they span more than one
    line. When aligning parameters is not appropriate due to line-length
    constraints, single indent for the lines after the first is also
    acceptable.
<sup>[[link](#no-double-indent)]</sup>

  ```Ruby
  # starting point (line is too long)
  def send_mail(source)
    Mailer.deliver(to: 'bob@example.com', from: 'us@example.com', subject: 'Important message', body: source.text)
  end

  # bad (double indent)
  def send_mail(source)
    Mailer.deliver(
        to: 'bob@example.com',
        from: 'us@example.com',
        subject: 'Important message',
        body: source.text)
  end

  # good
  def send_mail(source)
    Mailer.deliver(to: 'bob@example.com',
                   from: 'us@example.com',
                   subject: 'Important message',
                   body: source.text)
  end

  # good (normal indent)
  def send_mail(source)
    Mailer.deliver(
      to: 'bob@example.com',
      from: 'us@example.com',
      subject: 'Important message',
      body: source.text
    )
  end
  ```

* <a name="align-multiline-arrays"></a>
  Align the elements of array literals spanning multiple lines.
<sup>[[link](#align-multiline-arrays)]</sup>

  ```Ruby
  # bad - single indent
  menu_item = ['Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam',
    'Baked beans', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam']

  # good
  menu_item = [
    'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam',
    'Baked beans', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam'
  ]

  # good
  menu_item =
    ['Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam',
     'Baked beans', 'Spam', 'Spam', 'Spam', 'Spam', 'Spam']
  ```

* <a name="underscores-in-numerics"></a>
  Add underscores to large numeric literals to improve their readability.
<sup>[[link](#underscores-in-numerics)]</sup>

  ```Ruby
  # bad - how many 0s are there?
  num = 1000000

  # good - much easier to parse for the human brain
  num = 1_000_000
  ```

* <a name="120-character-limits"></a>
  Limit lines to 120 characters.
<sup>[[link](#120-character-limits)]</sup>

* <a name="no-trailing-whitespace"></a>
  Avoid trailing whitespace.
<sup>[[link](#no-trailing-whitespace)]</sup>

* <a name="newline-eof"></a>
  End each file with a newline.
<sup>[[link](#newline-eof)]</sup>

* <a name="no-block-comments"></a>
    Don't use block comments. They cannot be preceded by whitespace and are not
    as easy to spot as regular comments.
<sup>[[link](#no-block-comments)]</sup>

  ```Ruby
  # bad
  =begin
  comment line
  another comment line
  =end

  # good
  # comment line
  # another comment line
  ```
