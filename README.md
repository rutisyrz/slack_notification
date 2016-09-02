# slack_notification
Demo app - Receive Staging/Production exception notifications in Slack Channel

## Required gems 
- [exception_notification](https://rubygems.org/gems/exception_notification), [slack-notifier](https://rubygems.org/gems/slack-notifier)

## Prerequisite

- Create a channel named “*exceptions*” in your Slack account
- Get Web Hook URL - [click here](https://github.com/stevenosloan/slack-notifier#setting-defaults)

## Integrate Slack Notification in your Rails app

- Add required gems in Gemfile
```ruby
gem ‘exception_notification’
gem ‘slack-notifier’
```

- Install bundle
```ruby
bundle install
```

- Add below code in /config/environments/staging.rb file 
```ruby
config.middleware.use ExceptionNotification::Rack,  
  slack: {
    webhook_url: "https://YOUR-SLACK-WEB-HOOK-URL",
    channel: "#exceptions",
    username: "staging-exception", # ENV based username to distinguish Staging Exceptions in channel
    additional_parameters: { 
      icon_emoji: ":large_blue_circle:",  # BLUE CIRCLE icon to distinguish Staging Exceptions in channel
      mrkdwn: true 
    } 
  }
```

- Add below code in /config/environments/production.rb file 
```ruby
config.middleware.use ExceptionNotification::Rack,  
  slack: {
    webhook_url: "https://YOUR-SLACK-WEB-HOOK-URL",
    channel: "#exceptions",
    username: "production-exception", # ENV based username to distinguish Production Exceptions in channel
    additional_parameters: { 
      icon_emoji: ":red_circle:",  # RED CIRCLE icon to distinguish Production Exceptions in channel
      mrkdwn: true 
    } 
  }
```
