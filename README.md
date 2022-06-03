# README

## Docker

https://matsuand.github.io/docs.docker.jp.onthefly/samples/rails/

## About

This README would normally document whatever steps are necessary to get the
application up and running.

Things you may want to cover:

* Ruby version

* System dependencies

* Configuration

* Database creation

* Database initialization

* How to run the test suite

* Services (job queues, cache servers, search engines, etc.)

* Deployment instructions

* ...

## MEMO

Rubyのバージョンを3系，Railsを7系にアップデートしたらエラー

```bash
web_1  | 
web_1  | ERROR: It looks like you're trying to use Nokogiri as a precompiled native gem on a system with glibc < 2.17:
web_1  | 
web_1  |   /lib/aarch64-linux-gnu/libm.so.6: version `GLIBC_2.29' not found (required by /usr/local/bundle/gems/nokogiri-1.13.6-aarch64-linux/lib/nokogiri/3.1/nokogiri.so) - /usr/local/bundle/gems/nokogiri-1.13.6-aarch64-linux/lib/nokogiri/3.1/nokogiri.so
web_1  | 
web_1  |   If that's the case, then please install Nokogiri via the `ruby` platform gem:
web_1  |       gem install nokogiri --platform=ruby
web_1  |   or:
web_1  |       bundle config set force_ruby_platform true
web_1  | 
web_1  |   Please visit https://nokogiri.org/tutorials/installing_nokogiri.html for more help.
web_1  | 
web_1  | 
web_1  | ERROR: It looks like you're trying to use Nokogiri as a precompiled native gem on a system with glibc < 2.17:
web_1  | 
web_1  |   /lib/aarch64-linux-gnu/libm.so.6: version `GLIBC_2.29' not found (required by /usr/local/bundle/gems/nokogiri-1.13.6-aarch64-linux/lib/nokogiri/3.1/nokogiri.so) - /usr/local/bundle/gems/nokogiri-1.13.6-aarch64-linux/lib/nokogiri/3.1/nokogiri.so
```

下記サイトに解決方法
https://abillyz.com/watanabe/studies/244

Dockerfileに

```Dockerfile
bundle config set force_ruby_platform true && \
```

を追記

`docker-conpose up --build`で別のエラー

```bash
web_1  | => Booting Puma
web_1  | => Rails 7.0.3 application starting in development 
web_1  | => Run `bin/rails server --help` for more startup options
web_1  | Exiting
web_1  | /myapp/config/initializers/new_framework_defaults.rb:21:in `<top (required)>': undefined method `halt_callback_chains_on_return_false=' for ActiveSupport:Module (NoMethodError)
web_1  | 
web_1  | ActiveSupport.halt_callback_chains_on_return_false = false
web_1  |              ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
web_1  |        from /usr/local/bundle/gems/railties-7.0.3/lib/rails/engine.rb:667:in `load'
web_1  |        from /usr/local/bundle/gems/railties-7.0.3/lib/rails/engine.rb:667:in `block in load_config_initializer'
web_1  |        from /usr/local/bundle/gems/activesupport-7.0.3/lib/active_support/notifications.rb:208:in `instrument'
web_1  |        from /usr/local/bundle/gems/railties-7.0.3/lib/rails/engine.rb:666:in `load_config_initializer'
web_1  |        from /usr/local/bundle/gems/railties-7.0.3/lib/rails/engine.rb:620:in `block (2 levels) in <class:Engine>'
web_1  |        from /usr/local/bundle/gems/railties-7.0.3/lib/rails/engine.rb:619:in `each'
web_1  |        from /usr/local/bundle/gems/railties-7.0.3/lib/rails/engine.rb:619:in `block in <class:Engine>'
web_1  |        from /usr/local/bundle/gems/railties-7.0.3/lib/rails/initializable.rb:32:in `instance_exec'
web_1  |        from /usr/local/bundle/gems/railties-7.0.3/lib/rails/initializable.rb:32:in `run'
web_1  |        from /usr/local/bundle/gems/railties-7.0.3/lib/rails/initializable.rb:61:in `block in run_initializers'
web_1  |        from /usr/local/lib/ruby/3.1.0/tsort.rb:228:in `block in tsort_each'
web_1  |        from /usr/local/lib/ruby/3.1.0/tsort.rb:350:in `block (2 levels) in each_strongly_connected_component'
web_1  |        from /usr/local/lib/ruby/3.1.0/tsort.rb:422:in `block (2 levels) in each_strongly_connected_component_from'
web_1  |        from /usr/local/lib/ruby/3.1.0/tsort.rb:431:in `each_strongly_connected_component_from'
web_1  |        from /usr/local/lib/ruby/3.1.0/tsort.rb:421:in `block in each_strongly_connected_component_from'
web_1  |        from /usr/local/bundle/gems/railties-7.0.3/lib/rails/initializable.rb:50:in `each'
web_1  |        from /usr/local/bundle/gems/railties-7.0.3/lib/rails/initializable.rb:50:in `tsort_each_child'
web_1  |        from /usr/local/lib/ruby/3.1.0/tsort.rb:415:in `call'
web_1  |        from /usr/local/lib/ruby/3.1.0/tsort.rb:415:in `each_strongly_connected_component_from'
web_1  |        from /usr/local/lib/ruby/3.1.0/tsort.rb:349:in `block in each_strongly_connected_component'
web_1  |        from /usr/local/lib/ruby/3.1.0/tsort.rb:347:in `each'
web_1  |        from /usr/local/lib/ruby/3.1.0/tsort.rb:347:in `call'
web_1  |        from /usr/local/lib/ruby/3.1.0/tsort.rb:347:in `each_strongly_connected_component'
web_1  |        from /usr/local/lib/ruby/3.1.0/tsort.rb:226:in `tsort_each'
web_1  |        from /usr/local/lib/ruby/3.1.0/tsort.rb:205:in `tsort_each'
web_1  |        from /usr/local/bundle/gems/railties-7.0.3/lib/rails/initializable.rb:60:in `run_initializers'
web_1  |        from /usr/local/bundle/gems/railties-7.0.3/lib/rails/application.rb:372:in `initialize!'
web_1  |        from /myapp/config/environment.rb:5:in `<top (required)>'
web_1  |        from config.ru:3:in `require_relative'
web_1  |        from config.ru:3:in `block in <main>'
web_1  |        from /usr/local/bundle/gems/rack-2.2.3.1/lib/rack/builder.rb:116:in `eval'
web_1  |        from /usr/local/bundle/gems/rack-2.2.3.1/lib/rack/builder.rb:116:in `new_from_string'
web_1  |        from /usr/local/bundle/gems/rack-2.2.3.1/lib/rack/builder.rb:105:in `load_file'
web_1  |        from /usr/local/bundle/gems/rack-2.2.3.1/lib/rack/builder.rb:66:in `parse_file'
web_1  |        from /usr/local/bundle/gems/rack-2.2.3.1/lib/rack/server.rb:349:in `build_app_and_options_from_config'
web_1  |        from /usr/local/bundle/gems/rack-2.2.3.1/lib/rack/server.rb:249:in `app'
web_1  |        from /usr/local/bundle/gems/rack-2.2.3.1/lib/rack/server.rb:422:in `wrapped_app'
web_1  |        from /usr/local/bundle/gems/railties-7.0.3/lib/rails/commands/server/server_command.rb:76:in `log_to_stdout'
web_1  |        from /usr/local/bundle/gems/railties-7.0.3/lib/rails/commands/server/server_command.rb:36:in `start'
web_1  |        from /usr/local/bundle/gems/railties-7.0.3/lib/rails/commands/server/server_command.rb:143:in `block in perform'
web_1  |        from <internal:kernel>:90:in `tap'
web_1  |        from /usr/local/bundle/gems/railties-7.0.3/lib/rails/commands/server/server_command.rb:134:in `perform'
web_1  |        from /usr/local/bundle/gems/thor-1.2.1/lib/thor/command.rb:27:in `run'
web_1  |        from /usr/local/bundle/gems/thor-1.2.1/lib/thor/invocation.rb:127:in `invoke_command'
web_1  |        from /usr/local/bundle/gems/thor-1.2.1/lib/thor.rb:392:in `dispatch'
web_1  |        from /usr/local/bundle/gems/railties-7.0.3/lib/rails/command/base.rb:87:in `perform'
web_1  |        from /usr/local/bundle/gems/railties-7.0.3/lib/rails/command.rb:48:in `invoke'
web_1  |        from /usr/local/bundle/gems/railties-7.0.3/lib/rails/commands.rb:18:in `<top (required)>'
web_1  |        from /myapp/bin/rails:9:in `require'
web_1  |        from /myapp/bin/rails:9:in `<top (required)>'
web_1  |        from /usr/local/bundle/gems/spring-2.1.1/lib/spring/client/rails.rb:28:in `load'
web_1  |        from /usr/local/bundle/gems/spring-2.1.1/lib/spring/client/rails.rb:28:in `call'
web_1  |        from /usr/local/bundle/gems/spring-2.1.1/lib/spring/client/command.rb:7:in `call'
web_1  |        from /usr/local/bundle/gems/spring-2.1.1/lib/spring/client.rb:30:in `run'
web_1  |        from /usr/local/bundle/gems/spring-2.1.1/bin/spring:49:in `<top (required)>'
web_1  |        from /usr/local/bundle/gems/spring-2.1.1/lib/spring/binstub.rb:11:in `load'
web_1  |        from /usr/local/bundle/gems/spring-2.1.1/lib/spring/binstub.rb:11:in `<top (required)>'
web_1  |        from /myapp/bin/spring:15:in `require'
web_1  |        from /myapp/bin/spring:15:in `<top (required)>'
web_1  |        from bin/rails:3:in `load'
web_1  |        from bin/rails:3:in `<main>'
```

検索したら下記ヒット
https://qiita.com/Tatsuru12/items/530195d3bc071d558d45

該当箇所コメントアウトして`docker-compose up --build`したら起動した
