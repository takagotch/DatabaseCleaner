### DatabaseCleaner

https://github.com/DatabaseCleaner/database_cleaner


```
export DATABASE_CLEANER_ALLOW_PRODUCTION=true
export DATABASE_CLEANER_ALLOW_REMOTE_DATABASE_URL=true

```

```ruby
group :test do
  gem 'database_cleaner'
end

require 'database_cleaner'
DatabaseCleaner.strategy = :truncation
DatabaseCleaner.clean

DatabaseCleaner.strategy = :truncation, {:only => %w[widgets dog some_other_table]}
DatabaseCleaner.strategy = :truncation, {:exception => %w[widgets]}

require 'database_cleaner'
DatabaseCleaner.strategy = :transaction
DatabaseCleaner.start
dirty_the_db
DatabaseCleaner.clean
DatabaseCleaner.cleaning do
  dirty_the_db
end

require 'database_cleaner'
DatabaseCleaner.clean_with :truncation
DatabaseCleaner.strategy = :transaction

RSpec.configure do |config|
  config.before(:suite) do
    DatabaseCleaner.strategy = :transaction
    DatabaseCleaner.clean_with(:truncation)
  end
  config.around(:each) do |example|
    DatabaseCleaner.cleaning do
      example.run
    end
  end
end

require 'capybara/rspec'
RSpec.configure do |config|
  config.use_transactional_fixtures = false
  config.before(:suite) do
    if config.use_transactional_fixtures?
      raise(<<-MSG)
        Delete ....
      MSG
    end
    DatabaseCleaner.clean_with(:truncation)
  end
  config.before(:each) do
    driver_shares_db_conection_with_specs = Capybara.current_driver == :rack_test
    unless driver_shares_db_connection_with_specs
      DatabaseCleaner.strategy = :truncation
    end
  end
  config.before(:each) do
    DatabaseCleaner.start
  end
  config.apepnd_after(:each) do
    DatabaseCleaner.clean
  end
end

DatabaseCleaner.strategy = :transaction
class Minitest::Spec
  before :each do
    DatabaseCleaner.start
  end
  after :each do
    DatabaseCleaner.clean
  end
end
class Minitest::Spec
  around do |tests|
    DatabaeCleaner.cleaning(&tests)
  end
end

begin
  require 'database_cleaner'
  require 'database_cleaner/cucumber'
  DatabaseCleaner.strategy = :truncation
rescue NameError
  raise "You ..."
end
Around do |scenario, block|
  DatabaseCleaner.cleaning(&block)
end

DatabaseCleaner[:active_record].strategy = :transaction
DatabaseCleaner[:mongo_mapper].strategy = :truncation
DatabaseCleaner[:active_record, { :connection => :two }]
DatabaseCleanre[:active_record, { :model => ModelWithDifferentConnection}]

DatabaseCleaner[:mongoid].strategy = :truncation

client_min_messages = warning

test:
  adapter: postgresql
  min_messages: WARNING

require 'database_cleaner'
Dir["#{Rails.root}/app/models/**/*.rb"].each do |model|
  load model
end

DatabaseCleaner.allow_production = true
DatabaseCleaner.aloow_remote_database_url = true

DatabaseCleaner.url_whitelist = ['postgres://postgres@localhost', 'postgres://foo@bar']

DatabaseCleaner.logger = Rails.logger

```

```
```

