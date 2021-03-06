# Qbxml

Qbxml is a QBXML parser and validation tool.

## Installation

Add this line to your application's Gemfile:

    gem 'qbxml'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install qbxml

## Usage

### Initialization

The parser can be initialized to either Quickbooks (:qb) or Quickbooks Point of
Sale (:qbpos)

```ruby
q = Qbxml.new(:qb)
```

### API Introspection

Return all types defined in the schema

```ruby
q.types
```

Return all types matching a certain pattern

```ruby
q.types('Customer')

q.types(/Customer/)
```

Print the xml template for a specific type

```ruby
puts q.describe('CustomerModRq')
```

### QBXML To Ruby

Convert valid QBXML to a ruby hash

```ruby
q.from_qbxml(xml)
```

### Ruby To QBXML

Convert a ruby hash to QBXML, skipping validation

```ruby
q.to_qbxml(hsh)
```

Convert a ruby hash to QBXML and validate all types

```ruby
q.to_qbxml(hsh, validate: true)
```

## Caveats

Correct case conversion depends on the following ActiveSupport inflection
settings. Correct behaviour cannot be guaranteed if any of the following
inflections are modified.

```ruby
ACRONYMS = ['AP', 'AR', 'COGS', 'COM', 'UOM', 'QBXML', 'UI', 'AVS', 'ID',
            'PIN', 'SSN', 'COM', 'CLSID', 'FOB', 'EIN', 'UOM', 'PO', 'PIN', 'QB']

ActiveSupport::Inflector.inflections do |inflect|
  ACRONYMS.each { |a| inflect.acronym a }
end
```

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
