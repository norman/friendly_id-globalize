# FriendlyId Globalize

[Globalize](https://github.com/globalize/globalize) support for
[FriendlyId](https://github.com/norman/friendly_id).

### Installation
```ruby
gem 'friendly_id-globalize'
rails generate friendly_id_globalize
```

### Translating Slugs Using Globalize
The `FriendlyId::Globalize Globalize` module lets you use
[Globalize](https://github.com/globalize/globalize) to translate slugs. This
module is most suitable for applications that need to be localized to many
languages. If your application only needs to be localized to one or two
languages, you may wish to consider the `FriendlyId::SimpleI18n SimpleI18n`
module.

In order to use this module, your model's table and translation table must both
have a slug column, and your model must set the `slug` field as translatable
with Globalize:
```ruby
class Post < ActiveRecord::Base
  translates :title, :slug
  extend FriendlyId
  friendly_id :title, :use => :globalize
end
```
Note that call to `translates` must be made before calling `friendly_id`.

### Finds
Finds will take the current locale into consideration:
```ruby
I18n.locale = :it
Post.find("guerre-stellari")
I18n.locale = :en
Post.find("star-wars")
```
Additionally, finds will fall back to the default locale:
```ruby
I18n.locale = :it
Post.find("star-wars")
```
To find a slug by an explicit locale, perform the find inside a block
passed to I18n's `with_locale` method:
```ruby
I18n.with_locale(:it) { Post.find("guerre-stellari") }
```
### Creating Records
When new records are created, the slug is generated for the current locale only.
### Translating Slugs
To translate an existing record's friendly_id, use
`FriendlyId::Globalize::Model#set_friendly_id`. This will ensure that the slug
you add is properly escaped, transliterated and sequenced:
```ruby
post = Post.create :name => "Star Wars"
post.set_friendly_id("Guerre stellari", :it)
```
If you don't pass in a locale argument, `FriendlyId::Globalize` will just use the
current locale:
```ruby
I18n.with_locale(:it) { post.set_friendly_id("Guerre stellari") }
```
