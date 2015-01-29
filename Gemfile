source 'https://rubygems.org'

gemspec

# Database Configuration
group :development, :test do
  gem "globalize", git: "https://github.com/globalize/globalize", branch: "rails-4-2-upgrade"
  gem 'rake'

  platforms :jruby do
    gem 'activerecord-jdbcsqlite3-adapter', '>= 1.3.0.beta2'
    gem 'jruby-openssl'
  end

  platforms :ruby do
    gem 'sqlite3'
  end

  gem 'pry'
  gem 'pry-nav'
end

