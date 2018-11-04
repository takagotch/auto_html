### auto_html
---
https://github.com/dejan/auto_html

```
gem 'auto_html'
bundle
gem install auto_html
```

```ruby
link_filter = AutoHtml::Link.new(target: '_blank')
link_filter.call('Checkout out my blog: http://rors.org')

emoji_filter = AutoHtml::Emoji.new
emoji_filter.call(':point_left: yo!')

base_format = AutoHtml::Pipeline.new(link_filter, emoji_filter)
base_format.call('Checkout out my blog: http://rors.org :point_left: yo!')

comment_format = AutoHtml::Pipeline.new(AutoHtml::Markdown.new, AutoHtml::Image.new, base_format)
comment_format.call("Hello!\n\n Checkout out my blog: http://roros.org :point_left: yo! \n\n http://gifs.joelgovier.com/boom/booyah.gif")

class Comment < ActiveRecord::Base
  FORMAT = AutoHtml::Pipeline.new(
    AutoHtml::HtmlEscape.new,
    AutoHtml::Markdown.new
  )
  def text=(t)
    super(t)
    self[:text_html] = FORMAT.call(t)
  end
end

comment = Comment.new(text: 'Hey!')
comment.text_html

```

```
```
