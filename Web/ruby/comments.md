# Creating and showing comments in 2-level-nests

### routes.rb > resources

```
# Resources
  resources :sessions
  resources :users
  resources :bookmarks

  resources :questions do
    resources :answers do
        resources :comments, shallow: true 
    end
  end
```

Shallowly nest resource to prevent deep nesting.

### Models

##### question.rb

```
class Question < ApplicationRecord    
    has_many :answers
    has_many :bookmarks
end
```

##### answer.rb

```
class Answer < ApplicationRecord
    belongs_to :question
    has_many :comments, as: :commentable

    has_many :likes, as: :likeable
    validates :answercontent, length: {minimum: 50}
end
```

use 'as: :commentable' to show the polymorphic relationship. An 'answer' will be a 'commentable' object.

##### comment.rb

```
class Comment < ApplicationRecord
    belongs_to :commentable, polymorphic: true
end
```

### View (show.html.erb)

The view shows the question on top, answers below, then comments below each answer.

```
<!-- Comments -->
  <% answer.comments.each do |comment| %>
   <%= comment.content %>
   <br>
  <% end %>
                            
<!-- Submit new comment -->
  <%= form_for Comment.new,url: question_answer_comments_path(@question,answer) do |f| %>
    <%= f.text_area :content %>
    <%= f.submit "Submit" %>
  <% end %>
```

This line was difficult for me to reach (someone on SO gave me this answer):
```
<%= form_for Comment.new, url: question_answer_comments_path(@question, answer) do |f| %>
```
I had to first, show which controller and action the form is for by specifying 'Comment.new'
Then, I had to specify the accurate path at 'question_answer_comments_path', not the 'new_question_answer_comments_path'
Finally, I had to pass in the correct params, as my comment requires the qn and answer id.

### Comments Controller

```
def new
    @comments = @commentable.comments
    @comment = @comments.new
end
  
def create
    @question = Question.find(params[:question_id])
    @commentable = Answer.find(params[:answer_id])
    @comments = @commentable.comments
    @comment = @comments.new(comment_params)
    
    if @comment.save
      redirect_to @question
    else
      render :new
    end
end
```

Where the comment_params are the private strong params.

