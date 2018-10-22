# RailsAdminShrine

Install and configure [shrine](https://github.com/shrinerb/shrine).

Suppose your model looks like this:

```ruby
class Article < ActiveRecord::Base
  include ImageUploader.attachment(:asset)
end
```

You can specify the field as a **'shrine'** type if not detected:

```ruby
  field :asset, :shrine
```

## Deleting attachment

You need to define a **delete method** if you want to delete attachment:

```ruby
class Article < ActiveRecord::Base
  include ImageUploader.attachment(:asset)
  
  attr_accessor :remove_asset
  after_save do
    next unless remove_asset == '1'
    self.remove_asset = nil
    update(image: nil)
  end
end
```

The method name is `remove_#{name}` by default, but you can configure it using `delete_method` option:

```ruby
field :asset, :shrine do
  delete_method :delete_asset
end
```

### This project rocks and uses MIT-LICENSE.
