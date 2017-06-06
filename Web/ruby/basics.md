
1. Start 

```
$rails new APPNAME
```

2. Create controller

```
$rails g controller CONTROLLERNAME
app/controllers/CONTROLLERNAME_controller.rb

  def VIEWNAME (i.e., index)
  end
```

3. Create View

```
views/CONTROLLERNAME/VIEWNAME.html.erb
```

4. Create routes

```
config/routes.rb
get '/' => 'CONTROLLERNAME#VIEWNAME'
```

5. Install Gems

Straigt from terminal:

```
gem install GEMNAME
```

Using gemfile:

```
gem 'GEMNAME'
$bundle install
```

