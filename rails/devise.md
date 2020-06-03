# Rails Auth with Devise

Devise is one of two popular rails user auth gems.

We will be implementing user auth with this library.

We will follow instuctions from the devise website: [https://github.com/plataformatec/devise](https://github.com/plataformatec/devise)

## Clone the base app

The base app is a one model rails app. You can insert and see each record. It has an index page.

[https://github.com/wdi-sg/user-songs](https://github.com/wdi-sg/user-songs)

```text
git clone https://github.com/wdi-sg/user-songs.git
cd user-songs
```

Install the app and run it to see that it works. Create and view some songs.

```text
bundle install
rails db:create
rails db:migrate
rails s
```

## Install Devise

Add the gem devise to the Gemfile

```text
gem 'devise'
```

Install it

```text
bundle install
```

Run the gem's script files so it can generate the default files in the rails app

```text
rails generate devise:install
```

Create the devise user model:

```text
rails generate devise user
```

Link User to a new foreign key column in songs:

```text
rails g migration AddUserToSongs user:references
```

\( if you give a migration name of the form AddXXXToYYY it will create the `change` line in the migration file automatically for you \)

```text
rails db:migrate
```

Generate the default devise view files:

```text
rails g devise:views
```

Devise might ask you to copy the secret devise key into the initializer file: `config/initializers/devise.rb`

## Set up authorization:

Add a before action filter to the controller:

```text
before_action :authenticate_user!, :except => [ :show, :index ]
```

Restrict the new link in the songs index with the devise helper

```text
<% if user_signed_in? %>
<%= link_to 'New Song', new_song_path %>
<% end %>
```

## Other devise helpers:

### current\_user

Make a breakpoint \(byebug\) in the `index` song controller method.

Inside the console see the value of current\_user

```text
current_user.id
```

### user\_session

See the current value of `user_session`

```text
user_session
```

Set something in the user session

```text
user_session["song_cart"] = "Single Ladies"
```

Use `c` to continue out of the breakpoint.

Make another request.

See the value of `user_session` has been retained.

## Adding user associations

Change both model files

app/models/song.rb

```text
belongs_to :user
```

app/models/user.rb

```text
has_many :song
```

Assign the logged in user as the song creator in app/controllers/songs\_controller.rb

```text
def create
  @song = Song.new(song_params)

  @song.user = current_user

  if @song.save
    redirect_to @song
  else
    render 'new'
  end
end
```

## Logout Link

```text
<%= link_to 'log out', destroy_user_session_url, method: :delete %>
```

## Login Link

```text
<%= link_to 'log in', new_user_session_url %>
```

