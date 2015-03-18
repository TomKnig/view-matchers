# view-matchers
RSpec-compatible testing matchers for common view contents.

* **[match_table](#match_table)**: write ascii-tables and match their existence
* **[match_form](#match_form)**: expressive matching for form fields

## Installation

Include the gem in your Gemfile:

```ruby
group :test do
  gem 'view-matchers'
end
```

## Matchers

view-matchers exposes some useful matchers for view specs. They are individually documented below.

#### match_table

You can match a table in a rendered view within a spec with `match_table`.

```ruby
# spec/views/table_spec.rb
it 'renders all products in a proper table' do
  expect(rendered).to match_table %(
    +----------+----------+----------+
    |   Number |  Product |    Price |
    +----------+----------+----------+
    |        1 | Computer |  42,00 € |
    +----------+----------+----------+
    |        2 |    Phone |  21,00 € |
    +----------+----------+----------+
  )
end
```

#### match_form

You can match a table in a rendered view within a spec with `match_form`.
`match_form` takes a `Proc` as argument. Methodnames within the `Proc` are interpreted as HTML-Tag matchers. The first parameter of these methods matches the `name` attribute, which can be followed by arbitrary attribute names and values. The last parameter is an optional block, that can be provided to match nested tags.

```ruby
# spec/views/sign_up_spec.rb
it 'renders a sign up form' do
  expect(rendered).to match_form proc {
    input 'user[email]', type: 'email'
    input 'user[password]', type: 'password'
    input 'user[password_confirmation]', type: 'password'
    select 'user[language]' do
      option nil, value: 'Objective-C'
      option nil, value: 'Swift'
    end
  }
end
```

## Contribution

I'd love to see your ideas!
I do really appreciate pull requests and [Github issues](https://github.com/TomKnig/view-matchers/issues/new). :octocat:

## Author

[Tom König](http://github.com/TomKnig) [@TomKnig](https://twitter.com/TomKnig)

## Versioning

view-matchers follows Semantic Versioning 2.0 as defined at <http://semver.org>.

## License

view-matchers is available under the MIT license. See the LICENSE file for more info.
