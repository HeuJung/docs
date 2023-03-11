# Eloquent: Relationships
# Eloquent: Relationships - 연관관계

- [Introduction](#introduction)
- [시작하기](#introduction)
- [Defining Relationships](#defining-relationships)
- [연관관계 정의하기](#defining-relationships)
    - [One To One](#one-to-one)
    - [1:1(일대일) 연관관계](#one-to-one)
    - [One To Many](#one-to-many)
    - [1:N(일대다) 연관관계](#one-to-many)
    - [One To Many (Inverse) / Belongs To](#one-to-many-inverse)
    - [1:N(일대다) 역연관관계](#one-to-many)
    - [Has One Of Many](#has-one-of-many)
    - [다수중 하나의 연관관계](#has-one-of-many)
    - [Has One Through](#has-one-through)
    - [연결을 통한 단일 연관관계](#has-one-through)
    - [Has Many Through](#has-many-through)
    - [연결을 통한 다수를 가지는 연관관계](#has-many-through)
- [Many To Many Relationships](#many-to-many)
- [N:M(다대다) 연관연관관계](#many-to-many)
    - [Retrieving Intermediate Table Columns](#retrieving-intermediate-table-columns)
    - [중간 테이블 컬럼 조회하기](#retrieving-intermediate-table-columns)
    - [Filtering Queries Via Intermediate Table Columns](#filtering-queries-via-intermediate-table-columns)
    - [중간 테이블을 사용한 필터링 쿼리](#filtering-queries-via-intermediate-table-columns)
    - [Ordering Queries Via Intermediate Table Columns](#ordering-queries-via-intermediate-table-columns)
    - [중간 테이블 컬럼을 통한 쿼리 정렬](#ordering-queries-via-intermediate-table-columns)
    - [Defining Custom Intermediate Table Models](#defining-custom-intermediate-table-models)
    - [커스텀 중간 테이블 모델 정의하기](#defining-custom-intermediate-table-models)
- [Polymorphic Relationships](#polymorphic-relationships)
- [다형성 연관관계](#polymorphic-relationships)
    - [One To One](#one-to-one-polymorphic-relations)
    - [1:1(일대일) 연관관계](#one-to-one-polymorphic-relations)
    - [One To Many](#one-to-many-polymorphic-relations)
    - [1:N(일대다) 연관관계](#one-to-many-polymorphic-relations)
    - [One Of Many](#one-of-many-polymorphic-relations)
    - [다수중 하나의 연관관계](#one-of-many-polymorphic-relations)
    - [Many To Many](#many-to-many-polymorphic-relations)
    - [N:M(다대다) 연관관계](#many-to-many-polymorphic-relations)
    - [Custom Polymorphic Types](#custom-polymorphic-types)
    - [사용자 정의 다형성 타입](#custom-polymorphic-types)
- [Dynamic Relationships](#dynamic-relationships)
- [동적 연관관계](#dynamic-relationships)
- [Querying Relations](#querying-relations)
- [연관관계 쿼리 질의하기](#querying-relations)
    - [Relationship Methods Vs. Dynamic Properties](#relationship-methods-vs-dynamic-properties)
    - [연관관계 메서드 Vs. 동적 속성](#relationship-methods-vs-dynamic-properties)
    - [Querying Relationship Existence](#querying-relationship-existence)
    - [존재하는 연관관계에 대한 쿼리 질의하기](#querying-relationship-existence)
    - [Querying Relationship Absence](#querying-relationship-absence)
    - [연관관계된 모델이 존재하지 않는 것을 확인하며 질의하기](#querying-relationship-absence)
    - [Querying Morph To Relationships](#querying-morph-to-relationships)
    - [다형성 연관관계 쿼리](#querying-morph-to-relationships)
- [Aggregating Related Models](#aggregating-related-models)
- [연관된 모델에 대한 집계쿼리 질의](#aggregating-related-models)
    - [Counting Related Models](#counting-related-models)
    - [연관된 모델 카운트 확인하기](#counting-related-models)
    - [Other Aggregate Functions](#other-aggregate-functions)
    - [기타 집계 함수들](#other-aggregate-functions)
    - [Counting Related Models On Morph To Relationships](#counting-related-models-on-morph-to-relationships)
    - [다형성 연관관계에서 관련된 모델 카운트 확인하기](#counting-related-models-on-morph-to-relationships)
- [Eager Loading](#eager-loading)
- [Eager 로딩](#eager-loading)
    - [Constraining Eager Loads](#constraining-eager-loads)
    - [Eager 로딩 조건 제한하기](#constraining-eager-loads)
    - [Lazy Eager Loading](#lazy-eager-loading)
    - [지연 Eager 로딩](#lazy-eager-loading)
    - [Preventing Lazy Loading](#preventing-lazy-loading)
    - [지연 로딩 방지하기](#preventing-lazy-loading)
- [Inserting & Updating Related Models](#inserting-and-updating-related-models)
- [연관된 모델 삽입하기](#inserting-and-updating-related-models)
    - [The `save` Method](#the-save-method)
    - [`save` 메서드](#the-save-method)
    - [The `create` Method](#the-create-method)
    - [`create` 메서드](#the-create-method)
    - [Belongs To Relationships](#updating-belongs-to-relationships)
    - [소속된 연관관계](#updating-belongs-to-relationships)
    - [Many To Many Relationships](#updating-many-to-many-relationships)
    - [다대다 연관관계](#updating-many-to-many-relationships)
- [Touching Parent Timestamps](#touching-parent-timestamps)
- [상위 모델의 타임스탬프 값 갱신하기](#touching-parent-timestamps)

<a name="introduction"></a>
## Introduction
## 시작하기

Database tables are often related to one another. For example, a blog post may have many comments or an order could be related to the user who placed it. Eloquent makes managing and working with these relationships easy, and supports a variety of common relationships:

데이터베이스의 테이블은 서로 연관되어 있습니다. 예를 들어, 블로그의 게시물이 여러개의 댓글을 가지고 있거나, 어떤 주문내역이 주문을 요청한 사용자와 연관되어 있을 수 있습니다. 엘로퀀트는 이러한 관계를 쉽게 관리하고 필요한 작업을 처리할 수 있는 다양한 유형의 연관관계를 지원합니다.

- [One To One](#one-to-one)
- [1:1(일대일) 연관관계](#one-to-one)
- [One To Many](#one-to-many)
- [1:N(일대다) 연관관계](#one-to-many)
- [Many To Many](#many-to-many)
- [N:M(다대다) 연관관계](#many-to-many)
- [Has One Through](#has-one-through)
- [연결을 통한 단일 연관관계](#has-one-through)
- [Has Many Through](#has-many-through)
- [연결을 통한 다수를 가지는 연관관계](#has-many-through)
- [One To One (Polymorphic)](#one-to-one-polymorphic-relations)
- [1:1(일대일) (다형성)](#one-to-one-polymorphic-relations)
- [One To Many (Polymorphic)](#one-to-many-polymorphic-relations)
- [1:N(일대다) (다형성)](#one-to-many-polymorphic-relations)
- [Many To Many (Polymorphic)](#many-to-many-polymorphic-relations)
- [N:M(다대다) (다형성)](#many-to-many-polymorphic-relations)

<a name="defining-relationships"></a>
## Defining Relationships
## 연관관계 정의하기

Eloquent relationships are defined as methods on your Eloquent model classes. Since relationships also serve as powerful [query builders](/docs/{{version}}/queries), defining relationships as methods provides powerful method chaining and querying capabilities. For example, we may chain additional query constraints on this `posts` relationship:

엘로퀀트 연관관계는 엘로퀀트 모델 클래스에 메서드로 정의합니다. 연관관계를 정의한 메서드는 그 자체로도 강력한 [쿼리 빌더](/docs/{{version}}/queries)로써의 기능으로도 작동하기 때문에 체이닝과 쿼리 그 자체로도 활용이 가능합니다. 예를 들어, 다음의 `posts` 연관관계에 쿼리 제약 조건을 추가할 수 있습니다.

    $user->posts()->where('active', 1)->get();

But, before diving too deep into using relationships, let's learn how to define each type of relationship supported by Eloquent.

연관관계를 사용하는 법을 알아보기 전에, 엘로퀀트에서 지원하는 연관관계 타입을 어떻게 정의하는지 알아보겠습니다.

<a name="one-to-one"></a>
### One To One
### 1:1(일대일) 연관관계 정의하기

A one-to-one relationship is a very basic type of database relationship. For example, a `User` model might be associated with one `Phone` model. To define this relationship, we will place a `phone` method on the `User` model. The `phone` method should call the `hasOne` method and return its result. The `hasOne` method is available to your model via the model's `Illuminate\Database\Eloquent\Model` base class:

일대일 연관관계는 아주 기본적인 타입의 데이터베이스 연관관계입니다. 예를 들어, 하나의 `User` 모델이 하나의 `Phone`과 연관되어 있을 수 있습니다. 이 연관관계를 정의하려면 `User` 모델에 `phone` 메서드를 추가하면 됩니다. `phone` 메서드는 `hasOne` 메서드를 호출하고 결과를 반환해야 합니다. `hasOne` 메서드는 `Illuminate\Database\Eloquent\Model` 기본 모델을 통해서 사용할 수 있습니다. 

    <?php

    namespace App\Models;

    use Illuminate\Database\Eloquent\Model;
    use Illuminate\Database\Eloquent\Relations\HasOne;

    class User extends Model
    {
        /**
         * Get the phone associated with the user.
         */
        public function phone(): HasOne
        {
            return $this->hasOne(Phone::class);
        }
    }

The first argument passed to the `hasOne` method is the name of the related model class. Once the relationship is defined, we may retrieve the related record using Eloquent's dynamic properties. Dynamic properties allow you to access relationship methods as if they were properties defined on the model:

`hasOne` 메서드에 전달되는 첫번째 인자는 관련된 모델 클래스의 이름입니다. 연관관계를 정의했다면, 엘로퀀트의 동적 속성을 이용하여 관련된 레코드를 찾을 수 있습니다. 동적 속성은 모델에 정의된 속성에 접근하는 방식과 같은 방식으로 연관관계 메서드에 접근하는 것을 허용합니다.

    $phone = User::find(1)->phone;

Eloquent determines the foreign key of the relationship based on the parent model name. In this case, the `Phone` model is automatically assumed to have a `user_id` foreign key. If you wish to override this convention, you may pass a second argument to the `hasOne` method:

엘로퀀트는 상위 모델 이름을 기반으로 연관관계의 외래 키(foreign key)를 결정합니다. 이 경우, `Phone` 모델은 `user_id` 외래 키를 가질 것이라고 자동으로 추정됩니다. 이 키를 재정의하고 싶다면, `hasOne` 메서드에 두번째 인자를 전달하면 됩니다.

    return $this->hasOne(Phone::class, 'foreign_key');

Additionally, Eloquent assumes that the foreign key should have a value matching the primary key column of the parent. In other words, Eloquent will look for the value of the user's `id` column in the `user_id` column of the `Phone` record. If you would like the relationship to use a primary key value other than `id` or your model's `$primaryKey` property, you may pass a third argument to the `hasOne` method:

추가적으로, 엘로퀀트는 외래 키가 상위 모델의 기본키(primary key) 컬럼에 상응하는 값을 가지고 있다고 추정합니다. 즉, 엘로퀀트는 `Phone` 레코드의 `user_id` 컬럼에서 사용자 `id` 컬럼의 값을 찾을 것입니다. 연관관계가 `id` 또는 모델의 `$primaryKey` 속성이 아닌 값을 사용하고자 한다면 세번째 인자로 커스텀 키를 `hasOne` 메서드로 전달하면 됩니다.

    return $this->hasOne(Phone::class, 'foreign_key', 'local_key');

<a name="one-to-one-defining-the-inverse-of-the-relationship"></a>
#### Defining The Inverse Of The Relationship
#### 연관관계의 역관계(반대) 정의하기

So, we can access the `Phone` model from our `User` model. Next, let's define a relationship on the `Phone` model that will let us access the user that owns the phone. We can define the inverse of a `hasOne` relationship using the `belongsTo` method:

이제 `User` 모델에서 `Phone` 모델에 접근할 수 있습니다. 반대로, `Phone` 모델에 연관관계를 정의하여 phone을 소유하는 user 에 접근할 수 있습니다. `belongsTo` 메서드를 이용하면 `hasOne` 연관관계의 역관계를 정의할 수 있습니다.

    <?php

    namespace App\Models;

    use Illuminate\Database\Eloquent\Model;
    use Illuminate\Database\Eloquent\Relations\BelongsTo;

    class Phone extends Model
    {
        /**
         * Get the user that owns the phone.
         */
        public function user(): BelongsTo
        {
            return $this->belongsTo(User::class);
        }
    }

When invoking the `user` method, Eloquent will attempt to find a `User` model that has an `id` which matches the `user_id` column on the `Phone` model.

`user` 메서드가 호출될 때, 엘로퀀트는 `Phone` 모델의 `user_id` 컬럼이 `User` 모델의 `id` 와 매칭되는지 확인합니다.

Eloquent determines the foreign key name by examining the name of the relationship method and suffixing the method name with `_id`. So, in this case, Eloquent assumes that the `Phone` model has a `user_id` column. However, if the foreign key on the `Phone` model is not `user_id`, you may pass a custom key name as the second argument to the `belongsTo` method:

엘로퀀트는 연관관계 메서드의 이름을 검사하고 메서드 이름에 `_id`를 붙여서 외래 키의 기본 이름으로 결정합니다. 따라서 위 예제에서는 엘로퀀트는 `Phone` 모델이 `user_id` 컬럼을 가지고 있다고 추정합니다. 하지만 `Phone` 모델의 외래 키가 `user_id`가 아닌 경우에는 커스텀 키의 이름을 `belongsTo` 메서드의 두번째 인자로 로 전달하면 됩니다.

    /**
     * Get the user that owns the phone.
     */
    public function user(): BelongsTo
    {
        return $this->belongsTo(User::class, 'foreign_key');
    }

If the parent model does not use `id` as its primary key, or you wish to find the associated model using a different column, you may pass a third argument to the `belongsTo` method specifying the parent table's custom key:

상위 모델이 `id`를 기본키로 사용하지 않거나 다른 컬럼을 사용하여 연관모델을 찾으려면 `belongsTo` 메서드의 세번째 인자로 커스텀 키이름을 전달하면 됩니다. 
    /**
     * Get the user that owns the phone.
     */
    public function user(): BelongsTo
    {
        return $this->belongsTo(User::class, 'foreign_key', 'owner_key');
    }

<a name="one-to-many"></a>
### One To Many
### 1:N(일대다) 연관관계 정의하기

A one-to-many relationship is used to define relationships where a single model is the parent to one or more child models. For example, a blog post may have an infinite number of comments. Like all other Eloquent relationships, one-to-many relationships are defined by defining a method on your Eloquent model:

일대다 연관관계는 다수의 하위 모델을 가지는 상위 모델의 연관성을 정의하는데 사용합니다. 예를 들어 한 블로그 게시물에는 댓글을 무제한으로 있을 수 있습니다. 다른 엘로퀀트 연관관계와 같이, 일대다 연관관계는 엘로퀀트 모델에서 제공하는 함수를 통해서 정의할 수 있습니다.

    <?php

    namespace App\Models;

    use Illuminate\Database\Eloquent\Model;
    use Illuminate\Database\Eloquent\Relations\HasMany;

    class Post extends Model
    {
        /**
         * Get the comments for the blog post.
         */
        public function comments(): HasMany
        {
            return $this->hasMany(Comment::class);
        }
    }

Remember, Eloquent will automatically determine the proper foreign key column for the `Comment` model. By convention, Eloquent will take the "snake case" name of the parent model and suffix it with `_id`. So, in this example, Eloquent will assume the foreign key column on the `Comment` model is `post_id`.

앞서 언급했듯이 엘로퀀트는 `Comment` 모델에 적절한 외래 키를 자동으로 결정합니다. 엘로퀀트는 관계에 따라서 상위 모델의 "snake case" 이름에 `_id`를 붙인 이름으로 키를 추정합니다. 따라서 이 예제에서 엘로퀀트는 `Comment` 모델의 외래 키 컬럼이 `post_id`일 것이라고 추정합니다.

Once the relationship method has been defined, we can access the [collection](/docs/{{version}}/eloquent-collections) of related comments by accessing the `comments` property. Remember, since Eloquent provides "dynamic relationship properties", we can access relationship methods as if they were defined as properties on the model:

연관관계를 정의하였다면, `comments` 속성에 접근하여 연관된 댓글 [컬렉션](/docs/{{version}}/eloquent-collections)에 엑세스 할 수 있습니다. 엘로퀀트가 "동적 연관관계 속성"을 지원하기 때문에, 모델에 속성이 정의된것과 같이 연관관계 메서드에 접근할 수 있습니다. 

    use App\Models\Post;

    $comments = Post::find(1)->comments;

    foreach ($comments as $comment) {
        // ...
    }

Since all relationships also serve as query builders, you may add further constraints to the relationship query by calling the `comments` method and continuing to chain conditions onto the query:

모든 연관관계는 쿼리 빌더의 역할도 가능하기 때문에, `comments` 메서드를 호출하고 쿼리에 조건을 계속 체이닝 하여 연관관계 쿼리에 제약조건을 추가할 수 있습니다. 

    $comment = Post::find(1)->comments()
                        ->where('title', 'foo')
                        ->first();

Like the `hasOne` method, you may also override the foreign and local keys by passing additional arguments to the `hasMany` method:

`hasOne` 메서드와 같이 `hasMany` 메서드에 추가적인 인자들을 전달하여 외래 및 로컬 키들을 재지정 할 수 있습니다.

    return $this->hasMany(Comment::class, 'foreign_key');

    return $this->hasMany(Comment::class, 'foreign_key', 'local_key');

<a name="one-to-many-inverse"></a>
### One To Many (Inverse) / Belongs To
### 1:N(일대다) 역관계

Now that we can access all of a post's comments, let's define a relationship to allow a comment to access its parent post. To define the inverse of a `hasMany` relationship, define a relationship method on the child model which calls the `belongsTo` method:

블로그 포스트웨 모든 댓글에 접근할 수 있어졌으니, 이번에느 댓글에서 상위 포스트에 접근하는 연관관계를 정의해보겠습니다. `hasMany` 연관관계의 역관계를 정의하려면 하위 모델에 `belongsTo` 메서드를 호출하는 연관관계 메서드를 정의하면 됩니다. 

    <?php

    namespace App\Models;

    use Illuminate\Database\Eloquent\Model;
    use Illuminate\Database\Eloquent\Relations\BelongsTo;

    class Comment extends Model
    {
        /**
         * Get the post that owns the comment.
         */
        public function post(): BelongsTo
        {
            return $this->belongsTo(Post::class);
        }
    }

Once the relationship has been defined, we can retrieve a comment's parent post by accessing the `post` "dynamic relationship property":

연관관계가 정의되었다면, 댓글 모델의 `post` 동적 연관관계 속성에 접근하여 상위 모델인 포스트를 조회할 수 있습니다.

    use App\Models\Comment;

    $comment = Comment::find(1);

    return $comment->post->title;

In the example above, Eloquent will attempt to find a `Post` model that has an `id` which matches the `post_id` column on the `Comment` model.

위의 예제에서 엘로퀀트는 `Comment` 모델의 `post_id` 와 `Post` 모델의 `id`이 매칭되는지 확인합니다. 

Eloquent determines the default foreign key name by examining the name of the relationship method and suffixing the method name with a `_` followed by the name of the parent model's primary key column. So, in this example, Eloquent will assume the `Post` model's foreign key on the `comments` table is `post_id`.

엘로퀀트는 연관관계 메서드의 이름을 확인하고 메서드 이름 뒤에 `_`와 기본키 컬럼의 이름을 붙여 외래키 이름을 결정합니다. 이 예제에서 엘로퀀트는 `comments` 테일에 존재하는 `Post` 모델의 외래키가 `post_id` 라고 가정합니다.

However, if the foreign key for your relationship does not follow these conventions, you may pass a custom foreign key name as the second argument to the `belongsTo` method:

만약 연관관계에 대한 외래키가 이러한 컨벤션을 따르지 않는 경우 `belongsTo` 메서드의 두 번째 인자로 커스텀 외래 키 이름을 전달하면 됩니다.

    /**
     * Get the post that owns the comment.
     */
    public function post(): BelongsTo
    {
        return $this->belongsTo(Post::class, 'foreign_key');
    }

If your parent model does not use `id` as its primary key, or you wish to find the associated model using a different column, you may pass a third argument to the `belongsTo` method specifying your parent table's custom key:

상위 모델이 `id`를 기본키로 사용하지 않거나, 다른 컬럼을 사용하여 연관된 모델을 찾고자 한다면 `belongsTo` 메서드의 세번째 인자로 상위 테이블의 커스텀 키를 전달하면 됩니다. 

    /**
     * Get the post that owns the comment.
     */
    public function post(): BelongsTo
    {
        return $this->belongsTo(Post::class, 'foreign_key', 'owner_key');
    }

<a name="default-models"></a>
#### Default Models
#### 기본 모델

The `belongsTo`, `hasOne`, `hasOneThrough`, and `morphOne` relationships allow you to define a default model that will be returned if the given relationship is `null`. This pattern is often referred to as the [Null Object pattern](https://en.wikipedia.org/wiki/Null_Object_pattern) and can help remove conditional checks in your code. In the following example, the `user` relation will return an empty `App\Models\User` model if no user is attached to the `Post` model:

`belongsTo`, `hasOne`, `hasOneThrough` 및 `morphOne` 연관관계를 사용하면 주어진 연관모델이 `null`인 경우 반환될 기본 모델을 정의할 수 있습니다. 이 패턴은 종종 [Null Object 패턴](https://en.wikipedia.org/wiki/Null_Object_pattern)이라고 하며 코드에서 널을 체크하는 조건식을 제거하는 데 도움이 됩니다. 다음 예제에서 `Post` 모델에 연관된 사용자가 없으면 `user` 관계는 비어있는 `App\Models\User` 모델을 반환합니다.

    /**
     * Get the author of the post.
     */
    public function user(): BelongsTo
    {
        return $this->belongsTo(User::class)->withDefault();
    }

To populate the default model with attributes, you may pass an array or closure to the `withDefault` method:

기본 모델에서 사용할 속성값을 지정하려면 `withDefault` 메서드에 배열이나 클로저를 전달하면 됩니다. 

    /**
     * Get the author of the post.
     */
    public function user(): BelongsTo
    {
        return $this->belongsTo(User::class)->withDefault([
            'name' => 'Guest Author',
        ]);
    }

    /**
     * Get the author of the post.
     */
    public function user(): BelongsTo
    {
        return $this->belongsTo(User::class)->withDefault(function (User $user, Post $post) {
            $user->name = 'Guest Author';
        });
    }

<a name="querying-belongs-to-relationships"></a>
#### Querying Belongs To Relationships
#### 일대다 역 연관관계에서 쿼리 질의하기

When querying for the children of a "belongs to" relationship, you may manually build the `where` clause to retrieve the corresponding Eloquent models:

"belongs to" 연관관계-(일대다의 역 연관관계)의 하위 모델에서 쿼리를 질의할 때, 일치하는 엘로퀀트 모델을 조회하기 위해서 `where` 메서드를 수동으로 추가할 수 있습니다. 

    use App\Models\Post;

    $posts = Post::where('user_id', $user->id)->get();

However, you may find it more convenient to use the `whereBelongsTo` method, which will automatically determine the proper relationship and foreign key for the given model:

또는 좀 더 편리한 방법으로 `whereBelongsTo`를 사용할 수도 있습니다. 이 메서드는 주어진 모델에 대한 외래키를 자동으로 결정합니다.

    $posts = Post::whereBelongsTo($user)->get();

You may also provide a [collection](/docs/{{version}}/eloquent-collections) instance to the `whereBelongsTo` method. When doing so, Laravel will retrieve models that belong to any of the parent models within the collection:

`whereBelongsTo` 메서드에 [컬렉션](/docs/{{version}}/eloquent-collections) 인스턴스를 전달할 수도 있습니다. 그렇게 하면, 라라벨은 컬렉션 내에 있는 모든 부모 모델과 연관된 모델을 조회할 것입니다.

    $users = User::where('vip', true)->get();

    $posts = Post::whereBelongsTo($users)->get();

By default, Laravel will determine the relationship associated with the given model based on the class name of the model; however, you may specify the relationship name manually by providing it as the second argument to the `whereBelongsTo` method:

기본적으로, 라라벨은 모델의 클래스 이름을 기반으로 주어진 모델과의 연관관계를 결정합니다. 수동으로 이 이름을 지정하려면 `whereBelongsTo` 메서드의 두번 째 인자로 이름을 전달하면 됩니다. 

    $posts = Post::whereBelongsTo($user, 'author')->get();

<a name="has-one-of-many"></a>
### Has One Of Many
### 일대다 중에서 하나를 표현하는 연관관계

Sometimes a model may have many related models, yet you want to easily retrieve the "latest" or "oldest" related model of the relationship. For example, a `User` model may be related to many `Order` models, but you want to define a convenient way to interact with the most recent order the user has placed. You may accomplish this using the `hasOne` relationship type combined with the `ofMany` methods:

때로는 모델이 여러개의 연관된 모델을 가질 수 있지만, 연관관계의 "최신의" 또는 "최고(가장 오래된)" 관련 모델을 조회하고 싶을 수 있습니다. 예를 들어 `User` 모델은 많은 `Order` 모델과 연관되어 있는데, 이 중에서 사용자가 가장 최근에 주문한 정보를 찾고자 하는 경우입니다. 이러한 경우에는 `ofMany` 메서드와 `hasOne` 연관관계 타입을 조합하여 사용하면 됩니다.

```php
/**
 * Get the user's most recent order.
 */
public function latestOrder(): HasOne
{
    return $this->hasOne(Order::class)->latestOfMany();
}
```

Likewise, you may define a method to retrieve the "oldest", or first, related model of a relationship:

마찬가지로, 연관관계의 "가장 오래된" 또는 제일 처음 연관관계를 형성한 모델을 조회하는 방법을 정의할 수도 있습니다. 

```php
/**
 * Get the user's oldest order.
 */
public function oldestOrder(): HasOne
{
    return $this->hasOne(Order::class)->oldestOfMany();
}
```

By default, the `latestOfMany` and `oldestOfMany` methods will retrieve the latest or oldest related model based on the model's primary key, which must be sortable. However, sometimes you may wish to retrieve a single model from a larger relationship using a different sorting criteria.

기본적으로 `latestOfMany`와 `oldestOfMany` 메서드가 모델의 기본키를 사용해서 가장 최신의 또는 가장 오래된 연관 모델을 조회할 때 이 기본키는 정렬이 가능해야합니다. 그렇지만 때로는 다른 정렬 기준을 사용하여 정렬하기를 원할 수도 있습니다.  

For example, using the `ofMany` method, you may retrieve the user's most expensive order. The `ofMany` method accepts the sortable column as its first argument and which aggregate function (`min` or `max`) to apply when querying for the related model:

예를 들어 `ofMany` 메서드를 사용하여 사용자의 가장 비싼 주문을 조회하려 할 수 있습니다. `ofMany` 메서드는 정렬 가능한 컬럼의 이름을 첫 번째 인자로, 연관 모델을 쿼리할 때 적용할 집계 함수(`min` 또는 `max`)를 두 번째 인자로 전달 받습니다.

```php
/**
 * Get the user's largest order.
 */
public function largestOrder(): HasOne
{
    return $this->hasOne(Order::class)->ofMany('price', 'max');
}
```

> **Warning**
> Because PostgreSQL does not support executing the `MAX` function against UUID columns, it is not currently possible to use one-of-many relationships in combination with PostgreSQL UUID columns.

> **Warning**
> PostgreSQL은 UUID 컬럼에 대해서 `MAX` 함수를 실행을 지원하지 않기 때문에, PostgreSQL UUID 컬럼과 함께 일대다 연관관계를 사용할수 없습니다. 

<a name="advanced-has-one-of-many-relationships"></a>
#### Advanced Has One Of Many Relationships
### 좀 더 복잡한 일대다 중에서 하나를 표현하는 연관관계

It is possible to construct more advanced "has one of many" relationships. For example, a `Product` model may have many associated `Price` models that are retained in the system even after new pricing is published. In addition, new pricing data for the product may be able to be published in advance to take effect at a future date via a `published_at` column.

좀 더 복잡한 "일대다 중에서 하나를 표현하는" 연관관계를 만드는 것도 가능합니다. 예를 들어 `Product` 모델에는 여러개의 `Price` 모델이 연관되어 있고 이중에 하나만 적용되는 구조를 가질 수도 있습니다. 추가적으로 제품-product에 대한 새로운 가격-price 데이터는 `published_at` 컬럼을 기준으로 미래에 적용되도록 할 수도 있습니다. 

So, in summary, we need to retrieve the latest published pricing where the published date is not in the future. In addition, if two prices have the same published date, we will prefer the price with the greatest ID. To accomplish this, we must pass an array to the `ofMany` method that contains the sortable columns which determine the latest price. In addition, a closure will be provided as the second argument to the `ofMany` method. This closure will be responsible for adding additional publish date constraints to the relationship query:

따라서 위의 경우를 요약하자면, 게시 날짜가 미래가 아닌 최신 가격정보를 확인할 수 있어야 합니다. 또한 만약 두개의 가격-price 가 동일한 게시날짜(published_at)를 가지고 있다면 ID 가 큰 경우가 적용되도록 해야합니다. 이런 요구사항을 달성하려면 최신 가격-price를 결정할 수 있는 컬럼(정렬이 가능한)과 ID를 포함한 배열을 `ofMany` 메서드에 전달해야합니다. 추가적으로 `ofMany` 메서드의 두번째 인자로 클로저를 전달해야하는데 이 클로저는 게시날짜에 대한 추가 조건을 연관관계 쿼리에 추가하는 역할을 수행합니다.  

```php
/**
 * Get the current pricing for the product.
 */
public function currentPricing(): HasOne
{
    return $this->hasOne(Price::class)->ofMany([
        'published_at' => 'max',
        'id' => 'max',
    ], function (Builder $query) {
        $query->where('published_at', '<', now());
    });
}
```

<a name="has-one-through"></a>
### Has One Through
### 연결을 통한 단일 연관관계

The "has-one-through" relationship defines a one-to-one relationship with another model. However, this relationship indicates that the declaring model can be matched with one instance of another model by proceeding _through_ a third model.

"연결을 통한 단일" 연관관계는 다른 모델을 거치는 일대일 연관관계를 말합니다. 이 연관관계는 선언하는 모델이 다른 모델의 인스턴스 하나와 매칭될 수 있다는 것을 나타냅니다. 

For example, in a vehicle repair shop application, each `Mechanic` model may be associated with one `Car` model, and each `Car` model may be associated with one `Owner` model. While the mechanic and the owner have no direct relationship within the database, the mechanic can access the owner _through_ the `Car` model. Let's look at the tables necessary to define this relationship:

예를 들어, 차량 정비점 애플리케이션에서 각각의 `Mechanic`(정비사) 모델은 하나의 `Car`(자동차) 모델과 연관관계를 가질 수 있고, 하나의 `Car`(자동차) 모델은 하나의 `Owner`(소유자) 모델과 연관되어 있다고 해보겠습니다. 정비사와 소유자는 데이터베이스 상에서는 직접적인 연관관계가 없지만, `Car` 모델을 _통하면_ 엑세스가 가능합니다. 이 연관관계를 정의하는데 필요한 테이블을 살펴보겠습니다.  

    mechanics
        id - integer
        name - string

    cars
        id - integer
        model - string
        mechanic_id - integer

    owners
        id - integer
        name - string
        car_id - integer

Now that we have examined the table structure for the relationship, let's define the relationship on the `Mechanic` model:

연관관계를 위한 테이블 구조를 살펴보았으니, 다음으로 `Mechanic` 모델에 연관관계를 정의해보겠습니다.  

    <?php

    namespace App\Models;

    use Illuminate\Database\Eloquent\Model;
    use Illuminate\Database\Eloquent\Relations\HasOneThrough;

    class Mechanic extends Model
    {
        /**
         * Get the car's owner.
         */
        public function carOwner(): HasOneThrough
        {
            return $this->hasOneThrough(Owner::class, Car::class);
        }
    }

The first argument passed to the `hasOneThrough` method is the name of the final model we wish to access, while the second argument is the name of the intermediate model.

`hasOneThrough` 메서드의 첫번째 인자는 엑세스 하고자 하는 최종 모델의 이름이 됩니다. 두 번재 인자는 연결을 맺어주는 중간 모델의 이름입니다.

Or, if the relevant relationships have already been defined on all of the models involved in the relationship, you may fluently define a "has-one-through" relationship by invoking the `through` method and supplying the names of those relationships. For example, if the `Mechanic` model has a `cars` relationship and the `Car` model has an `owner` relationship, you may define a "has-one-through" relationship connecting the mechanic and the owner like so:

또는 관계에 포함된 모든 모델에서 관련 관계가 이미 정의된 경우 `through` 메소드를 호출하고 해당 관계의 이름을 제공하여 "has-one-through" 관계를 편리하게 정의할 수 있습니다. 예를 들어, `Mechanic` 모델에 `cars` 관계가 있고 `Car` 모델에 `owner` 관계가 있는 경우 다음과 같이 정비사(mechanic)와 소유자(owner)를 연결하는 "has-one-through" 관계를 정의할 수 있습니다.

```php
// String based syntax...
return $this->through('cars')->has('owner');

// Dynamic syntax...
return $this->throughCars()->hasOwner();
```

<a name="has-one-through-key-conventions"></a>
#### Key Conventions
#### 키 컨벤션

Typical Eloquent foreign key conventions will be used when performing the relationship's queries. If you would like to customize the keys of the relationship, you may pass them as the third and fourth arguments to the `hasOneThrough` method. The third argument is the name of the foreign key on the intermediate model. The fourth argument is the name of the foreign key on the final model. The fifth argument is the local key, while the sixth argument is the local key of the intermediate model:

일반적으로 연관관계 쿼리를 수행할 때에는 엘로퀀트 외래 키 컨벤션이 사용됩니다. 연관관계 키를 커스텀하려면 `hasOneThrough` 메서드의 세번째, 네번재 인자로 키의 이름을 전달하면 됩니다. 세 번재 인자는 중간 모델의 외래 키 이름이고, 네 번재 인자는 최종 모델의 외래 키 이름입니다. 다섯 번째 인자는 로컬키의 이름, 여섯 번재 인자는 중간 모델의 로컬 키 이름입니다.

    class Mechanic extends Model
    {
        /**
         * Get the car's owner.
         */
        public function carOwner(): HasOneThrough
        {
            return $this->hasOneThrough(
                Owner::class,
                Car::class,
                'mechanic_id', // Foreign key on the cars table...
                'car_id', // Foreign key on the owners table...
                'id', // Local key on the mechanics table...
                'id' // Local key on the cars table...
            );
        }
    }

Or, as discussed earlier, if the relevant relationships have already been defined on all of the models involved in the relationship, you may fluently define a "has-one-through" relationship by invoking the `through` method and supplying the names of those relationships. This approach offers the advantage of reusing the key conventions already defined on the existing relationships:

또는 앞에서 설명한 것처럼 관련 관계가 관계에 포함된 모든 모델에 이미 정의된 경우 `through` 메소드를 호출하고 해당 관계의 이름을 제공하여 "has-one-through" 관계를 편리하게 정의할 수 있습니다. 이 접근 방식은 기존 관계에 이미 정의된 주요 규칙을 재사용할 수 있는 이점을 제공합니다.

```php
// String based syntax...
return $this->through('cars')->has('owner');

// Dynamic syntax...
return $this->throughCars()->hasOwner();
```

<a name="has-many-through"></a>
### Has Many Through
### 연결을 통한 다수를 가지는 연관관계 정의하기

The "has-many-through" relationship provides a convenient way to access distant relations via an intermediate relation. For example, let's assume we are building a deployment platform like [Laravel Vapor](https://vapor.laravel.com). A `Project` model might access many `Deployment` models through an intermediate `Environment` model. Using this example, you could easily gather all deployments for a given project. Let's look at the tables required to define this relationship:

"연결을 통한 다수를 가지는" 연관관계는 중간 테이블을 통해서, 서로 떨어진 연관관계 모델들(다수)에 접근하는 편리한 방법을 제공합니다. 예를 들어, [라라벨 Vapor](https://vapor.laravel.com)와 같은 배포 플랫폼을 제작한다고 가정해보겠습니다. 하나의 `Project` 모델은 `Environment` 중간 모델을 거쳐서 여러개의 `Deployment` 모델에 엑세스 할 수 있습니다. 이 예시를 적용해보면, 하나의 프로젝트(Project)에서 전체 배포(Deployment) 를 조회할 수 있습니다. 이 연관관계를 정의하기 위한 테이블 구조를 살펴보겠습니다.

    projects
        id - integer
        name - string

    environments
        id - integer
        project_id - integer
        name - string

    deployments
        id - integer
        environment_id - integer
        commit_hash - string

Now that we have examined the table structure for the relationship, let's define the relationship on the `Project` model:

이제 연관관계에 대한 테이블 구조를 살펴보았으니, `Project` 모델에 연관관계를 정의해보겠습니다.

    <?php

    namespace App\Models;

    use Illuminate\Database\Eloquent\Model;
    use Illuminate\Database\Eloquent\Relations\HasManyThrough;

    class Project extends Model
    {
        /**
         * Get all of the deployments for the project.
         */
        public function deployments(): HasManyThrough
        {
            return $this->hasManyThrough(Deployment::class, Environment::class);
        }
    }

The first argument passed to the `hasManyThrough` method is the name of the final model we wish to access, while the second argument is the name of the intermediate model.

`hasManyThrough` 메서드의 첫 번째 인자는 접근하고자 하는 최종 모델의 이름이고, 두 번째 인자는 중간 모델의 이름입니다.

Or, if the relevant relationships have already been defined on all of the models involved in the relationship, you may fluently define a "has-many-through" relationship by invoking the `through` method and supplying the names of those relationships. For example, if the `Project` model has a `environments` relationship and the `Environment` model has a `deployments` relationship, you may define a "has-many-through" relationship connecting the project and the deployments like so:

또는 관계에 포함된 모든 모델에서 관련 관계가 이미 정의된 경우 `through` 메소드를 호출하고 해당 관계의 이름을 제공하여 "has-many-through" 관계를 편리하게 정의할 수 있습니다. 예를 들어, `Project` 모델에 `environments` 관계가 있고 `Environment` 모델에 `deployments` 관계가 있는 경우 다음과 같이 프로젝트(project)와 배포(deployments)를 연결하는 "has-many-through" 관계를 정의할 수 있습니다.

```php
// String based syntax...
return $this->through('environments')->has('deployments');

// Dynamic syntax...
return $this->throughEnvironments()->hasDeployments();
```

Though the `Deployment` model's table does not contain a `project_id` column, the `hasManyThrough` relation provides access to a project's deployments via `$project->deployments`. To retrieve these models, Eloquent inspects the `project_id` column on the intermediate `Environment` model's table. After finding the relevant environment IDs, they are used to query the `Deployment` model's table.

`Deployment` 모델의 테이블에는 `project_id` 컬럼이 포함되어 있지 않지만 `hasManyThrough` 연관관계는 `$project->deployments`를 통해 프로젝트의 배포에 대해 접근이 가능하게 해줍니다. 이 모델들(배포 모델들)을 조회하기 위해서 엘로퀀트는 중간 모델 `Environment` 테이블의 `project_id` 컬럼을 확인합니다. 연관된 `Environment` 모델의 ID들을 찾은 다음에 `Deployment`(배포) 모델의 테이블을 쿼리하는 데 사용합니다.

<a name="has-many-through-key-conventions"></a>
#### Key Conventions
#### 키 컨벤션

Typical Eloquent foreign key conventions will be used when performing the relationship's queries. If you would like to customize the keys of the relationship, you may pass them as the third and fourth arguments to the `hasManyThrough` method. The third argument is the name of the foreign key on the intermediate model. The fourth argument is the name of the foreign key on the final model. The fifth argument is the local key, while the sixth argument is the local key of the intermediate model:

일반적으로 연관관계 쿼리를 수행할 때에는 엘로퀀트 외래 키 컨벤션이 사용됩니다. 연관관계 키를 커스텀하려면 `hasManyThrough` 메서드의 세번째, 네번재 인자로 키의 이름을 전달하면 됩니다. 세 번재 인자는 중간 모델의 외래 키 이름이고, 네 번재 인자는 최종 모델의 외래 키 이름입니다. 다섯 번째 인자는 로컬키의 이름, 여섯 번재 인자는 중간 모델의 로컬 키 이름입니다.

    class Project extends Model
    {
        public function deployments(): HasManyThrough
        {
            return $this->hasManyThrough(
                Deployment::class,
                Environment::class,
                'project_id', // Foreign key on the environments table...
                'environment_id', // Foreign key on the deployments table...
                'id', // Local key on the projects table...
                'id' // Local key on the environments table...
            );
        }
    }

Or, as discussed earlier, if the relevant relationships have already been defined on all of the models involved in the relationship, you may fluently define a "has-many-through" relationship by invoking the `through` method and supplying the names of those relationships. This approach offers the advantage of reusing the key conventions already defined on the existing relationships:

또는 앞에서 설명한 것처럼 관련 관계가 관계에 포함된 모든 모델에 이미 정의된 경우 `through` 메소드를 호출하고 해당 모델의 이름을 제공하여 "has-many-through" 관계를 편리하게 정의할 수 있습니다. 이 접근 방식은 기존 관계에 이미 정의된 주요 규칙을 재사용할 수 있는 이점을 제공합니다.

```php
// String based syntax...
return $this->through('environments')->has('deployments');

// Dynamic syntax...
return $this->throughEnvironments()->hasDeployments();
```

<a name="many-to-many"></a>
## Many To Many Relationships
## N:M (다대다) 연관관계

Many-to-many relations are slightly more complicated than `hasOne` and `hasMany` relationships. An example of a many-to-many relationship is a user that has many roles and those roles are also shared by other users in the application. For example, a user may be assigned the role of "Author" and "Editor"; however, those roles may also be assigned to other users as well. So, a user has many roles and a role has many users.

다대다 연관관계는 `hasOne` 및 `hasMany` 연관관계보다 약간 더 복잡합니다. 다대다 연관관계는 많은 역할(role)을 가지는 사용자(user)를 예로 들 수 있습니다. 역할은 하나의 사용자에게만 부여되는게 아니라 다른 사용자에게도 해당 역할을 공유할 수 있습니다ㅏ. 예를 들어 하나의 사용자는 "저자"의 역할과 "편집자"의 역할을 부여받을 수 있습니다. 동시에 이러한 역할은 다른 사용자에게도 부여할 수 있습니다. 따라서 하나의 사용자는 다수의 역할을 가지고 하나의 역할은 다수의 사용자에게 할당 될 수 있습니다. 

<a name="many-to-many-table-structure"></a>
#### Table Structure
#### Table 구조

To define this relationship, three database tables are needed: `users`, `roles`, and `role_user`. The `role_user` table is derived from the alphabetical order of the related model names and contains `user_id` and `role_id` columns. This table is used as an intermediate table linking the users and roles.

이 연관관계를 정의하려면 `users`, `roles`, `role_user`의 세 가지 데이터베이스 테이블이 필요합니다. `role_user` 테이블은 연관된 모델 이름의 알파벳 순서에서 파생되어 이름이 결정되었습니다. 이 테이블은 사용자와 역할 테이블을 연결하는 중간 테이블로 `user_id`, `role_id` 컬럼을 가지고 있습니다.

Remember, since a role can belong to many users, we cannot simply place a `user_id` column on the `roles` table. This would mean that a role could only belong to a single user. In order to provide support for roles being assigned to multiple users, the `role_user` table is needed. We can summarize the relationship's table structure like so:

역할은 다수의 사용자에게 부여될 수 있기 때문에, `roles` 테이블에는 `user_id` 컬럼을 추가할 수가 없습니다. 하나의 역할(role)은 하나의 사용자(user) 에게만 부여될 수 있습니다. 따라서 이 것은 역할이 다수의 사용자에게 부여되기 위해서는 `role_user` 라는 중간 테이블이 필요하다는 것을 의미합니다. 결과적으로 다대다 연관관계를 표현하는 테이블 구조는 다음과 같습니다. 

    users
        id - integer
        name - string

    roles
        id - integer
        name - string

    role_user
        user_id - integer
        role_id - integer

<a name="many-to-many-model-structure"></a>
#### Model Structure
#### 모델 구조

Many-to-many relationships are defined by writing a method that returns the result of the `belongsToMany` method. The `belongsToMany` method is provided by the `Illuminate\Database\Eloquent\Model` base class that is used by all of your application's Eloquent models. For example, let's define a `roles` method on our `User` model. The first argument passed to this method is the name of the related model class:

다대다 연관관계는 `belongsToMany` 메서드의 결과를 반환하는 메서드를 작성하여 정의합니다. `belongsToMany` 메서드는 애플리케이션의 모든 엘로퀀트 모델이 사용하는 `Illuminate\Database\Eloquent\Model` 기본 클래스에서 제공됩니다. 예를 들어 `User` 모델에 `roles` 메서드를 정의해보겠습니다. 이 메서드에 전달되는 첫 번째 인자는 연관 모델 클래스의 이름이 됩니다.  

    <?php

    namespace App\Models;

    use Illuminate\Database\Eloquent\Model;
    use Illuminate\Database\Eloquent\Relations\BelongsToMany;

    class User extends Model
    {
        /**
         * The roles that belong to the user.
         */
        public function roles(): BelongsToMany
        {
            return $this->belongsToMany(Role::class);
        }
    }

Once the relationship is defined, you may access the user's roles using the `roles` dynamic relationship property:

연관관계를 정의하였다면 동적 연관관계 속성 `roles`을 사용하여 사용자의 역할들에 접근할 수 있습니다.

    use App\Models\User;

    $user = User::find(1);

    foreach ($user->roles as $role) {
        // ...
    }

Since all relationships also serve as query builders, you may add further constraints to the relationship query by calling the `roles` method and continuing to chain conditions onto the query:

모든 연관관계는 쿼리 빌더의 역할도 가능하기 때문에, `roles` 메서드를 호출하고 쿼리에 조건을 계속 체이닝 하여 연관관계 쿼리에 제약조건을 추가할 수 있습니다.

    $roles = User::find(1)->roles()->orderBy('name')->get();

To determine the table name of the relationship's intermediate table, Eloquent will join the two related model names in alphabetical order. However, you are free to override this convention. You may do so by passing a second argument to the `belongsToMany` method:

엘로퀀트는 연관관계의 중간 테이블의 이름을 결정하기 위해 연관된 두 모델 이름을 알파벳 순으로 조합합니다. (user 와 role 일 경우에 role_user 로 테이블 이름을 추정합니다) 하지만 이러한 관례는 오버라이딩 할 수 있습니다. `belongsToMany` 메서드의 두 번재 인자로 중간 테이블명을 전달하면 됩니다.

    return $this->belongsToMany(Role::class, 'role_user');

In addition to customizing the name of the intermediate table, you may also customize the column names of the keys on the table by passing additional arguments to the `belongsToMany` method. The third argument is the foreign key name of the model on which you are defining the relationship, while the fourth argument is the foreign key name of the model that you are joining to:

중간 테이블의 이름을 커스터마이징하는 것 외에도 `belongsToMany` 메서드에 추가 인자들을 전달하면 참조하는 키들의 이름들 또한 커스터마이징 할 수 있습니다. 세번째 인자는 연관관계를 정의하는 모델의 외래 키 이름이고 네번째 인자는 조인 하는 모델의 외래 키 이름입니다.

    return $this->belongsToMany(Role::class, 'role_user', 'user_id', 'role_id');

<a name="many-to-many-defining-the-inverse-of-the-relationship"></a>
#### Defining The Inverse Of The Relationship
#### 다대다 연관관계의 역관계 정의하기

To define the "inverse" of a many-to-many relationship, you should define a method on the related model which also returns the result of the `belongsToMany` method. To complete our user / role example, let's define the `users` method on the `Role` model:

다대다 연관관계의 역관계를 정의하기 위해서는 연관된 모델에 `belongsToMany` 메서드의 결과를 호출하는 연관관계 메서드를 정의하면 됩니다. 계속해서 사용자 / 역할 예제를 생각해보면 다음과 같이 `Role` 모델에 `users` 메서드를 정의하면 됩니다.

    <?php

    namespace App\Models;

    use Illuminate\Database\Eloquent\Model;
    use Illuminate\Database\Eloquent\Relations\BelongsToMany;

    class Role extends Model
    {
        /**
         * The users that belong to the role.
         */
        public function users(): BelongsToMany
        {
            return $this->belongsToMany(User::class);
        }
    }

As you can see, the relationship is defined exactly the same as its `User` model counterpart with the exception of referencing the `App\Models\User` model. Since we're reusing the `belongsToMany` method, all of the usual table and key customization options are available when defining the "inverse" of many-to-many relationships.

위에서 볼 수 있듯이 연관관계 메서드가 `App\Models\User` 모델을 참고하는 것만 제외하고 대응하는 `User`와 정확히 동일하게 정의되어 있습니다. `belongsToMany` 메서드를 재사용하고 있기 때문에 다대다 연관관계의 "역관계"를 정의할 때에도 테이블과 키 지정등 일반적인 커스터마이징 옵션을 사용 가능합니다.

<a name="retrieving-intermediate-table-columns"></a>
### Retrieving Intermediate Table Columns
### 중간 테이블 컬럼 조회하기

As you have already learned, working with many-to-many relations requires the presence of an intermediate table. Eloquent provides some very helpful ways of interacting with this table. For example, let's assume our `User` model has many `Role` models that it is related to. After accessing this relationship, we may access the intermediate table using the `pivot` attribute on the models:

앞서 살펴보았듯이, 다대다 연관관계는 중간 테이블을 필요로 합니다. 엘로퀀트는 중간 테이블을 조작할 수 있도록 도움을 주는 몇몇 방법들을 제공합니다. 예를 들어, `User` 객체가 여러 `Role` 객체에 관련되어 있다고 생각해 보면, 이 연관관계에 접근한 후 모델들의 `pivot` 속성을 사용하여 중간 테이블에 접근할 수 있습니다.

    use App\Models\User;

    $user = User::find(1);

    foreach ($user->roles as $role) {
        echo $role->pivot->created_at;
    }

Notice that each `Role` model we retrieve is automatically assigned a `pivot` attribute. This attribute contains a model representing the intermediate table.

연관관계를 통해서 조회된 `Role` 모델은 자동으로 `pivot` 속성을 부여받습니다. 이 속성은 중간 테이블을 나타내는 모델을 포함하고 있습니다. 

By default, only the model keys will be present on the `pivot` model. If your intermediate table contains extra attributes, you must specify them when defining the relationship:

기본적으로는, `pivot` 모델에는 연관된 모델의 키만 존재합니다. 만약 중간테이블에 추가적인 속성을 포함시킨다면 연관관계를 정의할 때 이를 지정해야만 합니다.

    return $this->belongsToMany(Role::class)->withPivot('active', 'created_by');

If you would like your intermediate table to have `created_at` and `updated_at` timestamps that are automatically maintained by Eloquent, call the `withTimestamps` method when defining the relationship:

중간테이블에 엘로퀀트에 의해서 자동으로 관리되는 `created_at`와 `updated_at` 타임스탬프 속성을 가지길 원한다면 연관관계 테이블을 정의할 때 `withTimestamps` 메서드를 호출하면 됩니다.

    return $this->belongsToMany(Role::class)->withTimestamps();

> **Warning**
> Intermediate tables that utilize Eloquent's automatically maintained timestamps are required to have both `created_at` and `updated_at` timestamp columns.

> **Warning**
> 엘로퀀트에 의해서 자동으로 관리되는 타임스탬프 속성을 사용하는 중간 테이블에는 `created_at`와 `updated_at` 타임스탬프 컬럼을 가지고 있어야 합니다. 

<a name="customizing-the-pivot-attribute-name"></a>
#### Customizing The `pivot` Attribute Name
#### `pivot` 속성의 이름 커스터마이징 하기

As noted previously, attributes from the intermediate table may be accessed on models via the `pivot` attribute. However, you are free to customize the name of this attribute to better reflect its purpose within your application.

앞서 언급한것 처럼 모델의 `pivot` 속성을 사용하여 중간 테이블의 속성에 접근할 수 있습니다. 그렇지만 애플리케이션에서 사용하는 용도에 적합하도록 속성의 이름을 커스터마이징 할 수 있습니다.

For example, if your application contains users that may subscribe to podcasts, you likely have a many-to-many relationship between users and podcasts. If this is the case, you may wish to rename your intermediate table attribute to `subscription` instead of `pivot`. This can be done using the `as` method when defining the relationship:

예를 들어, 사용자가 팟캐스트를 등록할 수 있는 경우 애플리케이션에서 사용자와 팟캐스트는 다대다 연관관계를 형성할 수 있습니다. 중간 테이블에 엑세스 하려면 원래는 `pivot` 을 사용하지만 이 경우에는 `subscription` 이라는 이름이 더 적합합니다. 연관관계를 정의할 때 `as` 메서드를 호출하면 커스터마이징하고자 하는 이름을 지정할 수 있습니다.   

    return $this->belongsToMany(Podcast::class)
                    ->as('subscription')
                    ->withTimestamps();

Once the custom intermediate table attribute has been specified, you may access the intermediate table data using the customized name:

중간테이블에 접근하고자 하는 이름을 커스터마이징하도록 지정한 뒤에는 이 이름을 사용해서 중간 테이블에 접근할 수 있습니다. 

    $users = User::with('podcasts')->get();

    foreach ($users->flatMap->podcasts as $podcast) {
        echo $podcast->subscription->created_at;
    }

<a name="filtering-queries-via-intermediate-table-columns"></a>
### Filtering Queries Via Intermediate Table Columns
### 중간 테이블의 컬럼을 사용한 연관관계의 필터 쿼리

You can also filter the results returned by `belongsToMany` relationship queries using the `wherePivot`, `wherePivotIn`, `wherePivotNotIn`, `wherePivotBetween`, `wherePivotNotBetween`, `wherePivotNull`, and `wherePivotNotNull` methods when defining the relationship:

`belongsToMany` 연관관계를 정의할 때 `wherePivot`, `wherePivotIn`, `wherePivotNotIn`, `wherePivotBetween`, `wherePivotNotBetween`, `wherePivotNull`, `wherePivotNotNull` 메서드를 사용하여 연관관계 쿼리에 결과를 필터링 할 수 있습니다.

    return $this->belongsToMany(Role::class)
                    ->wherePivot('approved', 1);

    return $this->belongsToMany(Role::class)
                    ->wherePivotIn('priority', [1, 2]);

    return $this->belongsToMany(Role::class)
                    ->wherePivotNotIn('priority', [1, 2]);

    return $this->belongsToMany(Podcast::class)
                    ->as('subscriptions')
                    ->wherePivotBetween('created_at', ['2020-01-01 00:00:00', '2020-12-31 00:00:00']);

    return $this->belongsToMany(Podcast::class)
                    ->as('subscriptions')
                    ->wherePivotNotBetween('created_at', ['2020-01-01 00:00:00', '2020-12-31 00:00:00']);

    return $this->belongsToMany(Podcast::class)
                    ->as('subscriptions')
                    ->wherePivotNull('expired_at');

    return $this->belongsToMany(Podcast::class)
                    ->as('subscriptions')
                    ->wherePivotNotNull('expired_at');

<a name="ordering-queries-via-intermediate-table-columns"></a>
### Ordering Queries Via Intermediate Table Columns
### 중간 테이블 컬럼을 통한 쿼리 정렬

You can order the results returned by `belongsToMany` relationship queries using the `orderByPivot` method. In the following example, we will retrieve all of the latest badges for the user:

`orderByPivot` 메서드를 이용해서 `belongsToMany` 관계 쿼리에 의해 반환된 결과를 정렬할 수 있습니다. 아래 예제는 사용자의 모든 뱆지를 역순으로 조회합니다.

    return $this->belongsToMany(Badge::class)
                    ->where('rank', 'gold')
                    ->orderByPivot('created_at', 'desc');

<a name="defining-custom-intermediate-table-models"></a>
### Defining Custom Intermediate Table Models
### 커스텀 중간 테이블 모델 정의하기

If you would like to define a custom model to represent the intermediate table of your many-to-many relationship, you may call the `using` method when defining the relationship. Custom pivot models give you the opportunity to define additional behavior on the pivot model, such as methods and casts.

다대다 연관관계의 중간 테이블을 표현하는 커스텀 모델을 정의할 수 있습니다. 이 때에는 연관관계를 정의할 때 `using` 메서드를 호출하면 됩니다. 커스텀 피벗 모델은 피벗 모델에 메서드나 casts.model 같은 추가적인 행위을 정의할 수 있게 해줍니다. 

Custom many-to-many pivot models should extend the `Illuminate\Database\Eloquent\Relations\Pivot` class while custom polymorphic many-to-many pivot models should extend the `Illuminate\Database\Eloquent\Relations\MorphPivot` class. For example, we may define a `Role` model which uses a custom `RoleUser` pivot model:

커스텀 다대다 피벗 모델은 `Illuminate\Database\Eloquent\Relations\Pivot` 클래스를 상속해야하며 커스텀 다형성 다대다 피벗 모델은 `Illuminate\Database\Eloquent\Relations\MorphPivot` 클래스를 상속해야합니다. 예를 들어 다음과 같이 커스텀 `RoleUser` 피벗 모델을 사용하는 `Role` 모델을 정의할 수 있습니다.

    <?php

    namespace App\Models;

    use Illuminate\Database\Eloquent\Model;
    use Illuminate\Database\Eloquent\Relations\BelongsToMany;

    class Role extends Model
    {
        /**
         * The users that belong to the role.
         */
        public function users(): BelongsToMany
        {
            return $this->belongsToMany(User::class)->using(RoleUser::class);
        }
    }

When defining the `RoleUser` model, you should extend the `Illuminate\Database\Eloquent\Relations\Pivot` class:

`RoleUser` 모델을 정의할 때에는 `Illuminate\Database\Eloquent\Relations\Pivot` 클래스를 상속해야합니다.

    <?php

    namespace App\Models;

    use Illuminate\Database\Eloquent\Relations\Pivot;

    class RoleUser extends Pivot
    {
        // ...
    }

> **Warning**
> Pivot models may not use the `SoftDeletes` trait. If you need to soft delete pivot records consider converting your pivot model to an actual Eloquent model.

> **Warning**
> 피벗 모델은 `SoftDeletes` 트레이트-trait을 사용하지 않습니다. 만약 모델의 레코드에 소프트 삭제기능을 사용해야 한다면, 피벗 모델이 아니라 기본적인 엘로퀀트 모델로 변환하는 것을 고려해보십시오.

<a name="custom-pivot-models-and-incrementing-ids"></a>
#### Custom Pivot Models And Incrementing IDs
#### 커스텀 피벗 모델과 자동증가 ID

If you have defined a many-to-many relationship that uses a custom pivot model, and that pivot model has an auto-incrementing primary key, you should ensure your custom pivot model class defines an `incrementing` property that is set to `true`.

커스텀 피벗 모델을 사용하는 다대다 연관관계를 정의하고 피벗 모델에 자동증가하는(auto incrementing) 기본 키가 있을 경우 커스텀 피벗 모델 클래스의 `incrementing` 속성이 `true`로 되어 있는지 확인해야 합니다.

    /**
     * Indicates if the IDs are auto-incrementing.
     *
     * @var bool
     */
    public $incrementing = true;

<a name="polymorphic-relationships"></a>
## Polymorphic Relationships
## 다형성 연관관계

A polymorphic relationship allows the child model to belong to more than one type of model using a single association. For example, imagine you are building an application that allows users to share blog posts and videos. In such an application, a `Comment` model might belong to both the `Post` and `Video` models.

다형성 연관관계란 하위 모델이 하나 이상의 모델타입과 연관될 때를 의미합니다. 예를 들어 애플리케이션에서 사용자가 블로그 포스트와 비디오를 공유하는 기능을 제공한다고 가정해보겠습니다. 공유된 `Post`(포스트)와 `Video`(비디오) 모두 `Comment`(댓글)이 연관관계를 형성할 수 있습니다.

<a name="one-to-one-polymorphic-relations"></a>
### One To One (Polymorphic)
### 1:1(일대일) (다형성)

<a name="one-to-one-polymorphic-table-structure"></a>
#### Table Structure
#### 테이블 구조

A one-to-one polymorphic relation is similar to a typical one-to-one relation; however, the child model can belong to more than one type of model using a single association. For example, a blog `Post` and a `User` may share a polymorphic relation to an `Image` model. Using a one-to-one polymorphic relation allows you to have a single table of unique images that may be associated with posts and users. First, let's examine the table structure:

일대일 다형성 연관관계는 기본적인 일대일 연관관계와 비슷합니다. 다만, 하위 모델과 연관되는 모델이 하나 이상의 타입이 될 수 있다는 점이 다릅니다. 예를 들자면, 블로그 `Post` 와 `User` 는 `Image` 모델에 다형성 연관관계를 서로 공유 할 수 있습니다. 일대일 다형성 연관관계를 사용한다면 블로그 포스트와 사용자 모델에 연관관계를 가지는 이미지 모델을 구성할 수 있습니다. 먼저 테이블 구조를 살펴보겠습니다.

    posts
        id - integer
        name - string

    users
        id - integer
        name - string

    images
        id - integer
        url - string
        imageable_id - integer
        imageable_type - string

Note the `imageable_id` and `imageable_type` columns on the `images` table. The `imageable_id` column will contain the ID value of the post or user, while the `imageable_type` column will contain the class name of the parent model. The `imageable_type` column is used by Eloquent to determine which "type" of parent model to return when accessing the `imageable` relation. In this case, the column would contain either `App\Models\Post` or `App\Models\User`.

`images` 테이블에서 `imageable_id` 와 `imageable_type` 컬럼을 주의깊게 살펴보십시오. `imageable_id` 컬럼은 포스트 ID 또는 사용자의 ID 값이 저장되고, `imageable_type` 컬럼에는 상위 모델 클래스의 이름이 저장됩니다. `imageable_type` 컬럼은 엘로퀀트가 `imageable` 연관관계에서 값을 반환할때 어떠한 "타입"의 모델과 연결해야 하는지 결정하는데 사용됩니다. 이 예제에서는 컬럼의 값이 `App\Models\Post` 또는 `App\Models\User`가 됩니다.

<a name="one-to-one-polymorphic-model-structure"></a>
#### Model Structure
#### 모델 구조

Next, let's examine the model definitions needed to build this relationship:

다음으로, 이러한 연관관계를 형성하기 위해서 모델에서 필요한 정의사항을 살펴보겠습니다.

    <?php

    namespace App\Models;

    use Illuminate\Database\Eloquent\Model;
    use Illuminate\Database\Eloquent\Relations\MorphTo;

    class Image extends Model
    {
        /**
         * Get the parent imageable model (user or post).
         */
        public function imageable(): MorphTo
        {
            return $this->morphTo();
        }
    }

    use Illuminate\Database\Eloquent\Model;
    use Illuminate\Database\Eloquent\Relations\MorphOne;

    class Post extends Model
    {
        /**
         * Get the post's image.
         */
        public function image(): MorphOne
        {
            return $this->morphOne(Image::class, 'imageable');
        }
    }

    use Illuminate\Database\Eloquent\Model;
    use Illuminate\Database\Eloquent\Relations\MorphOne;

    class User extends Model
    {
        /**
         * Get the user's image.
         */
        public function image(): MorphOne
        {
            return $this->morphOne(Image::class, 'imageable');
        }
    }

<a name="one-to-one-polymorphic-retrieving-the-relationship"></a>
#### Retrieving The Relationship
#### 연관관계 조회하기

Once your database table and models are defined, you may access the relationships via your models. For example, to retrieve the image for a post, we can access the `image` dynamic relationship property:

데이터베이스 테이블과 모델을 정의하고나면, 모델에서 연관관계에 엑세스 할 수 있습니다. 예를들어 포스트의 이미지를 조회한다면, `image` 라는 동적 연관관계 속성을 사용하면 됩니다.

    use App\Models\Post;

    $post = Post::find(1);

    $image = $post->image;

You may retrieve the parent of the polymorphic model by accessing the name of the method that performs the call to `morphTo`. In this case, that is the `imageable` method on the `Image` model. So, we will access that method as a dynamic relationship property:

`morphTo`를 호출하는 연관관계 메서드의 이름을 사용해서 다형성 모델의 상위 모델을 조회할 수 있습니다. 위의 예시에서는 `Image` 모델의 `imageable` 메서드가 해당 역할을 수행할 수 있습니다. 다음과 같이 동적 연관관계 속성에 접근할 수 있습니다.

    use App\Models\Image;

    $image = Image::find(1);

    $imageable = $image->imageable;

The `imageable` relation on the `Image` model will return either a `Post` or `User` instance, depending on which type of model owns the image.

`Image` 모델의 `imageable` 연관관계 속성은 이미지를 소유한 모델의 타입에 따라서 `Post` 또는 `User` 모델 인스턴스를 반환합니다.

<a name="morph-one-to-one-key-conventions"></a>
#### Key Conventions
#### 키 컨벤션

If necessary, you may specify the name of the "id" and "type" columns utilized by your polymorphic child model. If you do so, ensure that you always pass the name of the relationship as the first argument to the `morphTo` method. Typically, this value should match the method name, so you may use PHP's `__FUNCTION__` constant:

필요한 경우, 다형성 하위 모델에서 사용하는 "id"와 "type" 컬럼의 이름을 지정할 수 있습니다. 이 경우에는 `morphTo` 메서드의 첫 번재 인자로 연관관계의 이름을 전달해야 합니다. 일반적으로 이 값은 메서드의 이름과 일치해야 하기 때문에 PHP 의 `__FUNCTION__` 상수를 사용할 수 있습니다.  

    /**
     * Get the model that the image belongs to.
     */
    public function imageable(): MorphTo
    {
        return $this->morphTo(__FUNCTION__, 'imageable_type', 'imageable_id');
    }

<a name="one-to-many-polymorphic-relations"></a>
### One To Many (Polymorphic)
### 1:N(일대다) (다형성)

<a name="one-to-many-polymorphic-table-structure"></a>
#### Table Structure
#### 테이블 구조

A one-to-many polymorphic relation is similar to a typical one-to-many relation; however, the child model can belong to more than one type of model using a single association. For example, imagine users of your application can "comment" on posts and videos. Using polymorphic relationships, you may use a single `comments` table to contain comments for both posts and videos. First, let's examine the table structure required to build this relationship:

일대다 다형성 연관관계는 기본적인 일대다 연관관계와 유사합니다. 다만, 하위 모델과 연관되는 모델이 하나 이상의 타입이 될 수 있다는 점이 다릅니다. 예를 들자면, 블로그 포스트와 비디오에 모두 "댓글"을 달 수 있다고 생각해 보겠습니다. 다형성 연관관계를 사용하면 하나의 `comments` 테이블에서 포스트와 비디오 모두에 추가될 수 있는 댓들을 저장할 수 있습니다. 먼저 연관관계를 구성하기 위한 테이블 구조를 살펴보겠습니다.

    posts
        id - integer
        title - string
        body - text

    videos
        id - integer
        title - string
        url - string

    comments
        id - integer
        body - text
        commentable_id - integer
        commentable_type - string

<a name="one-to-many-polymorphic-model-structure"></a>
#### Model Structure
#### 모델 구조

Next, let's examine the model definitions needed to build this relationship:

다음으로 이 연관관계를 형성하기 위해 필요한 모델을 정의하는 방법을 살펴보겠습니다.

    <?php

    namespace App\Models;

    use Illuminate\Database\Eloquent\Model;
    use Illuminate\Database\Eloquent\Relations\MorphTo;

    class Comment extends Model
    {
        /**
         * Get the parent commentable model (post or video).
         */
        public function commentable(): MorphTo
        {
            return $this->morphTo();
        }
    }

    use Illuminate\Database\Eloquent\Model;
    use Illuminate\Database\Eloquent\Relations\MorphMany;

    class Post extends Model
    {
        /**
         * Get all of the post's comments.
         */
        public function comments(): MorphMany
        {
            return $this->morphMany(Comment::class, 'commentable');
        }
    }

    use Illuminate\Database\Eloquent\Model;
    use Illuminate\Database\Eloquent\Relations\MorphMany;

    class Video extends Model
    {
        /**
         * Get all of the video's comments.
         */
        public function comments(): MorphMany
        {
            return $this->morphMany(Comment::class, 'commentable');
        }
    }

<a name="one-to-many-polymorphic-retrieving-the-relationship"></a>
#### Retrieving The Relationship
#### 연관관계 조회하기

Once your database table and models are defined, you may access the relationships via your model's dynamic relationship properties. For example, to access all of the comments for a post, we can use the `comments` dynamic property:

데이터베이스 테이블과 모델이 정의되면 모델의 동적 연관관계 속성을 통해서 연관관계에 있는 하위 모델들에 접근할 수 있습니다. 예를들어 포스트의 댓글을 조회하려면 `comments` 동적 속성을 사용하면 됩니다.  

    use App\Models\Post;

    $post = Post::find(1);

    foreach ($post->comments as $comment) {
        // ...
    }

You may also retrieve the parent of a polymorphic child model by accessing the name of the method that performs the call to `morphTo`. In this case, that is the `commentable` method on the `Comment` model. So, we will access that method as a dynamic relationship property in order to access the comment's parent model:

`morphTo` 메서드를 호출하는 연관관계 메서드 이름을 사용해서 하위 다형성 모델에서 상위 모델을 조회할수도 있습니다. 이 예시에서는 `Comment` 모델의 `commentable` 연관관계 메서드가 됩니다. 따라서 다음과 같이 동적 연관관계 속성을 통해서 댓글의 상위 모델에 접근할 수 있습니다.  

    use App\Models\Comment;

    $comment = Comment::find(1);

    $commentable = $comment->commentable;

The `commentable` relation on the `Comment` model will return either a `Post` or `Video` instance, depending on which type of model is the comment's parent.

`Comment` 모델의 `commentable` 연관관계는 댓글을 소유한 모델 타입에 따라 `Post` 또는 `Video` 인스턴스를 반환합니다.

(역자주: 설명이 어렵지만 위의 예시에서 모델을 정의한 코드만 보면 `$comment->commentable()`의 연관관계 메서드를 정의해뒀지만 `$comment->commentable`와 같이 속성형태로 접근할 경우 라라벨이 자동으로 해당 댓글의 부모가 뭔지 찾아서 그에 맞는 객체를 가져와 준다는 의미입니다)

<a name="one-of-many-polymorphic-relations"></a>
### One Of Many (Polymorphic)
### 다수중 하나의 연관관계 (다형성)

Sometimes a model may have many related models, yet you want to easily retrieve the "latest" or "oldest" related model of the relationship. For example, a `User` model may be related to many `Image` models, but you want to define a convenient way to interact with the most recent image the user has uploaded. You may accomplish this using the `morphOne` relationship type combined with the `ofMany` methods:

때로는 모델이 여러개의 연관된 모델을 가질 수 있지만, 연관관계의 "최신의" 또는 "최고(가장 오래된)" 관련 모델을 조회하고 싶을 수 있습니다. 예를 들어 `User` 모델은 많은 `Image` 모델과 연관되어 있는데, 이 중에서 사용자가 가장 최근에 업로드한 이미지를 찾고자 하는 경우입니다. 이러한 경우에는 `ofMany` 메서드와 `morphOne` 연관관계 타입을 조합하여 사용하면 됩니다.

```php
/**
 * Get the user's most recent image.
 */
public function latestImage(): MorphOne
{
    return $this->morphOne(Image::class, 'imageable')->latestOfMany();
}
```

Likewise, you may define a method to retrieve the "oldest", or first, related model of a relationship:

마찬가지로, 연관관계의 "가장 오래된" 또는 제일 처음 연관관계를 형성한 모델을 조회하는 방법을 정의할 수도 있습니다.

```php
/**
 * Get the user's oldest image.
 */
public function oldestImage(): MorphOne
{
    return $this->morphOne(Image::class, 'imageable')->oldestOfMany();
}
```

By default, the `latestOfMany` and `oldestOfMany` methods will retrieve the latest or oldest related model based on the model's primary key, which must be sortable. However, sometimes you may wish to retrieve a single model from a larger relationship using a different sorting criteria.

기본적으로 `latestOfMany`와 `oldestOfMany` 메서드가 모델의 기본키를 사용해서 가장 최신의 또는 가장 오래된 연관 모델을 조회할 때 이 기본키는 정렬이 가능해야합니다. 그렇지만 때로는 다른 정렬 기준을 사용하여 정렬하기를 원할 수도 있습니다.

For example, using the `ofMany` method, you may retrieve the user's most "liked" image. The `ofMany` method accepts the sortable column as its first argument and which aggregate function (`min` or `max`) to apply when querying for the related model:

예를 들어 `ofMany` 메서드를 사용하여 가장 "좋아요"가 많은 사용자의 이미지를 조회하려 할 수 있습니다. `ofMany` 메서드는 정렬 가능한 컬럼의 이름을 첫 번째 인자로, 연관 모델을 쿼리할 때 적용할 집계 함수(`min` 또는 `max`)를 두 번째 인자로 전달 받습니다.

```php
/**
 * Get the user's most popular image.
 */
public function bestImage(): MorphOne
{
    return $this->morphOne(Image::class, 'imageable')->ofMany('likes', 'max');
}
```

> **Note**
> It is possible to construct more advanced "one of many" relationships. For more information, please consult the [has one of many documentation](#advanced-has-one-of-many-relationships).

> **Note**
> 보다 복잡한 경우의 "다수중 하나의" 연관관계에 대해서 알아보려면 [다수중 하나의 연관관계](#advanced-has-one-of-many-relationships) 매뉴얼을 참고하십시오.

<a name="many-to-many-polymorphic-relations"></a>
### Many To Many (Polymorphic)
### N:M(다대다) (다형성)

<a name="many-to-many-polymorphic-table-structure"></a>
#### Table Structure
#### 테이블 구조

Many-to-many polymorphic relations are slightly more complicated than "morph one" and "morph many" relationships. For example, a `Post` model and `Video` model could share a polymorphic relation to a `Tag` model. Using a many-to-many polymorphic relation in this situation would allow your application to have a single table of unique tags that may be associated with posts or videos. First, let's examine the table structure required to build this relationship:

다대다 다형성 연관관계는 "일대일 다형성"과 "일대다 다형성" 연관관계보다 더 복잡합니다. 예를 들어 하나의 `Post` 모델과 `Video` 모델이 다형성 `Tag` 모델과의 다형성 연관관계를 공유한다고 해보겠습니다. 이런경우에 다대다 다형성 연관관계를 사용하면 블로그 게시물(Post)과 비디오(Video)에 연결할 수 있는 고유한 태그를 저장하는 테이블을 하나만으로 처리할 수 있습니다. 먼저 연관관계를 구성하는 테이블 구조를 살펴보겠습니다.  

    posts
        id - integer
        name - string

    videos
        id - integer
        name - string

    tags
        id - integer
        name - string

    taggables
        tag_id - integer
        taggable_id - integer
        taggable_type - string

> **Note**
> Before diving into polymorphic many-to-many relationships, you may benefit from reading the documentation on typical [many-to-many relationships](#many-to-many).

> **Note**
> 다대다 다형성 연관관계에 대해서 알아보기 전에, 먼저 [다대다 연관관계](#many-to-many)에 대해서 숙지하는 것이 좋습니다. 

<a name="many-to-many-polymorphic-model-structure"></a>
#### Model Structure
#### 모델 구조

Next, we're ready to define the relationships on the models. The `Post` and `Video` models will both contain a `tags` method that calls the `morphToMany` method provided by the base Eloquent model class.

다음으로, 모델에 연관관계를 정의해보겠습니다. `Post` 및 `Video` 모델 클래스에 엘로퀀트 기본 모델 클래스에서 제공하는 `morphToMany` 메서드를 호출하는 `tags` 메서드를 추가합니다.

The `morphToMany` method accepts the name of the related model as well as the "relationship name". Based on the name we assigned to our intermediate table name and the keys it contains, we will refer to the relationship as "taggable":

`morphToMany` 메소드는 관련 모델의 이름과 "연관관계의 이름"을 인자로 전달 받습니다. 중간 테이블 이름에 할당한 이름과 여기에 포함된 키를 기반으로 관계를 "taggable"이라고 합니다.

    <?php

    namespace App\Models;

    use Illuminate\Database\Eloquent\Model;
    use Illuminate\Database\Eloquent\Relations\MorphToMany;

    class Post extends Model
    {
        /**
         * Get all of the tags for the post.
         */
        public function tags(): MorphToMany
        {
            return $this->morphToMany(Tag::class, 'taggable');
        }
    }

<a name="many-to-many-polymorphic-defining-the-inverse-of-the-relationship"></a>
#### Defining The Inverse Of The Relationship
#### 연관관계의 역관계 정의하기

Next, on the `Tag` model, you should define a method for each of its possible parent models. So, in this example, we will define a `posts` method and a `videos` method. Both of these methods should return the result of the `morphedByMany` method.

다음으로 `Tag` 모델에 각각의 상위모델이 될 수 있는 연관관계를 정의해야합니다. 따라서 이 예시에서는 `posts` 와 `videos` 메서드를 정의하면 됩니다. 이 두 메서드는 모두 `morphedByMany` 메서드의 결과를 반환해야 합니다.

The `morphedByMany` method accepts the name of the related model as well as the "relationship name". Based on the name we assigned to our intermediate table name and the keys it contains, we will refer to the relationship as "taggable":

`morphedByMany` 메서드는 연관관계 모델과 "연관관계의 이름"을 인자로 전달받습니다. 중간테이블 이름에 할당한 내용과 포함된 키를 기반으로 연관관계를 "taggable"이라고 했습니다.

    <?php

    namespace App\Models;

    use Illuminate\Database\Eloquent\Model;
    use Illuminate\Database\Eloquent\Relations\MorphToMany;

    class Tag extends Model
    {
        /**
         * Get all of the posts that are assigned this tag.
         */
        public function posts(): MorphToMany
        {
            return $this->morphedByMany(Post::class, 'taggable');
        }

        /**
         * Get all of the videos that are assigned this tag.
         */
        public function videos(): MorphToMany
        {
            return $this->morphedByMany(Video::class, 'taggable');
        }
    }

<a name="many-to-many-polymorphic-retrieving-the-relationship"></a>
#### Retrieving The Relationship
#### 연관관계 조회하기

Once your database table and models are defined, you may access the relationships via your models. For example, to access all of the tags for a post, you may use the `tags` dynamic relationship property:

데이터베이스 테이블과 모델을 정의하였다면, 이제 모델의 연관관계에 접근할 수 있습니다. 예를 들어 어떤 게시물의 모든 태그에 접근하려면 동적 연관관계 속성 `tags` 를 사용할 수 있습니다.

    use App\Models\Post;

    $post = Post::find(1);

    foreach ($post->tags as $tag) {
        // ...
    }

You may retrieve the parent of a polymorphic relation from the polymorphic child model by accessing the name of the method that performs the call to `morphedByMany`. In this case, that is the `posts` or `videos` methods on the `Tag` model:

`morphedByMany` 메서드를 호출하는 연관관계 메서드으 이름을 통해서 다형성 하위 모델에서 다형성 상위모델을 조회할 수 있습니다. 이 예시에서는 `Tag` 모델의 `posts` 또는 `videos` 메서드를 의미합니다. 

    use App\Models\Tag;

    $tag = Tag::find(1);

    foreach ($tag->posts as $post) {
        // ...
    }

    foreach ($tag->videos as $video) {
        // ...
    }

<a name="custom-polymorphic-types"></a>
### Custom Polymorphic Types
### 커스텀-사용자 정의 다형성 타입

By default, Laravel will use the fully qualified class name to store the "type" of the related model. For instance, given the one-to-many relationship example above where a `Comment` model may belong to a `Post` or a `Video` model, the default `commentable_type` would be either `App\Models\Post` or `App\Models\Video`, respectively. However, you may wish to decouple these values from your application's internal structure.

기본적으로, 라라벨은 관련된 모델의 유형을 저장하기 위해서 클래스의 정규화된 클래스 이름(qualified class name)을 사용합니다. 예를 들어 `Comment`모델이 하나의 `Post` 또는 하나의 `Video` 에 소속될 수 있는 일대일 연관관계가 주어지면, 기본적으로 `commentable_type`는 각각 `App\Models\Post` 또는 `App\Models\Video` 이 될 수 있습니다. 그렇지만, 애플리케이의 내부 구조에서 이런 값을 분리시킬 수 있습니다. 

For example, instead of using the model names as the "type", we may use simple strings such as `post` and `video`. By doing so, the polymorphic "type" column values in our database will remain valid even if the models are renamed:

예를 들어, 모델 이름을 "타입"으로 사용하는 대신 `post`, `video` 와 같은 간단한 문자열을 사용할 수 있습니다. 이렇게 하면 모델의 이름이 바뀌더라도 데이터베이스의 다형성 "type" 컬럼의 값이 계속 유지될 수 있는 장점이 있습니다. 

    use Illuminate\Database\Eloquent\Relations\Relation;

    Relation::enforceMorphMap([
        'post' => 'App\Models\Post',
        'video' => 'App\Models\Video',
    ]);

You may call the `enforceMorphMap` method in the `boot` method of your `App\Providers\AppServiceProvider` class or create a separate service provider if you wish.

`enforceMorphMap` 메서드 호출은 `App\Providers\AppServiceProvider`의 `boot` 메서드 또는 별도의 분리된 서비스프로바이더에서 처리할 수 있습니다.

You may determine the morph alias of a given model at runtime using the model's `getMorphClass` method. Conversely, you may determine the fully-qualified class name associated with a morph alias using the `Relation::getMorphedModel` method:

`getMorphClass` 메서드를 사용하여 런타임에 모델의 morph 별칭을 결정할 수 있습니다. 반대로 `Relation::getMorphedModel` 메서드를 사용하여 morph 별칭과 관련된 정규화 된 클래스 이름을 결정할 수 있습니다.

    use Illuminate\Database\Eloquent\Relations\Relation;

    $alias = $post->getMorphClass();

    $class = Relation::getMorphedModel($alias);

> **Warning**
> When adding a "morph map" to your existing application, every morphable `*_type` column value in your database that still contains a fully-qualified class will need to be converted to its "map" name.

> **Warning**
> 기존 애플리케이션에 "morph map"을 추가 할 때 정규화 된 클래스를 포함하고 있는 데이터베이스의 모든 변형 가능한 `*_type` 컬럼 값을 "map"이름으로 변환해야합니다.

<a name="dynamic-relationships"></a>
### Dynamic Relationships
### 동적 연관관계 정의하기

You may use the `resolveRelationUsing` method to define relations between Eloquent models at runtime. While not typically recommended for normal application development, this may occasionally be useful when developing Laravel packages.

`resolveRelationUsing` 메서드를 사용하면 런타임에 엘로퀀트 모델 사이의 연관관계를 정의할 수 있습니다. 일반적인 애플리케이션 개발에는 권장되지 않지만 라라벨 패키지를 개발할 때 유용 할 수 있습니다.

The `resolveRelationUsing` method accepts the desired relationship name as its first argument. The second argument passed to the method should be a closure that accepts the model instance and returns a valid Eloquent relationship definition. Typically, you should configure dynamic relationships within the boot method of a [service provider](/docs/{{version}}/providers):

`resolveRelationUsing` 메소드는 원하는 연관관계의 이름을 첫 번째 인자로 전달받습니다. 메서드에 전달된 두 번째 인자는 클로저인데 이 클로저는 모델 인스턴스를 인자로 받아 유효한 엘로퀀트 연관관계 정의를 반환해야합니다. 일반적으로 [서비스 프로바이더](/docs/{{version}}/providers)의 boot 메서드 안에서 동적 연관관계를 설정해야 합니다.

    use App\Models\Order;
    use App\Models\Customer;

    Order::resolveRelationUsing('customer', function (Order $orderModel) {
        return $orderModel->belongsTo(Customer::class, 'customer_id');
    });

> **Warning**
> When defining dynamic relationships, always provide explicit key name arguments to the Eloquent relationship methods.

> **Warning**
> 동적 연관관계를 정의 할 때에는 항상 엘로퀀트 연관관계 메서드에 명시적인 키 이름 인자를 제공하십시오.

<a name="querying-relations"></a>
## Querying Relations
## 연관관계 쿼리 질의하기

Since all Eloquent relationships are defined via methods, you may call those methods to obtain an instance of the relationship without actually executing a query to load the related models. In addition, all types of Eloquent relationships also serve as [query builders](/docs/{{version}}/queries), allowing you to continue to chain constraints onto the relationship query before finally executing the SQL query against your database.

모든 엘로퀀트 연관관계는 메서드를 통해서 정의됩니다. 연관모델을 로딩하기 위해서 실제로 쿼리를 실행하는 대신에 이 메서드를 호출해서 연관관계 모델 인스턴스를 가져올 수 있습니다. 추가적으로 모든 타입의 엘로퀀트 연관관계를 정의한 메서드는 그 자체로도 강력한 [쿼리 빌더](/docs/{{version}}/queries)로써의 기능으로도 작동하기 때문에 최종적으로 SQL 쿼리를 실행하기 전에 연관관계 쿼리에 제약조건을 계속 체이닝해서 연결할 수 있습니다.

For example, imagine a blog application in which a `User` model has many associated `Post` models:

예를 들어, `User` 모델이 다수의 `Post` 모델을 가지는 연관관계를 구현한 블로그 애플리케이션을 생각해 보겠습니다.

    <?php

    namespace App\Models;

    use Illuminate\Database\Eloquent\Model;
    use Illuminate\Database\Eloquent\Relations\HasMany;

    class User extends Model
    {
        /**
         * Get all of the posts for the user.
         */
        public function posts(): HasMany
        {
            return $this->hasMany(Post::class);
        }
    }

You may query the `posts` relationship and add additional constraints to the relationship like so:

다음과 같이 `posts` 연관관계들을 쿼리하고 연관관계에 제약조건을 추가할 수 있습니다.

    use App\Models\User;

    $user = User::find(1);

    $user->posts()->where('active', 1)->get();

You are able to use any of the Laravel [query builder's](/docs/{{version}}/queries) methods on the relationship, so be sure to explore the query builder documentation to learn about all of the methods that are available to you.

라라벨에서 제공하는 그 어떤 [쿼리 빌더](/docs/{{version}}/queries) 메서드라도 연관관계 메서드에 연결할 수 있기 때문에, 가능한 메서드들에 대해서 확인하려면 쿼리 빌더에 대한 문서를 확인하시기 바랍니다.

<a name="chaining-orwhere-clauses-after-relationships"></a>
#### Chaining `orWhere` Clauses After Relationships
#### 연관관계 메서드에 `orWhere` 절 연결하기

As demonstrated in the example above, you are free to add additional constraints to relationships when querying them. However, use caution when chaining `orWhere` clauses onto a relationship, as the `orWhere` clauses will be logically grouped at the same level as the relationship constraint:

위의 예시에서 설명한 것처럼 쿼리를 수행할 때 연관관계 메서드에 제약 조건을 추가 할 수 있습니다. 그러나 `orWhere` 절을 연관관계 메서드에 제약조건으로 추가할 때에는 연관관계를 조회하기 위한 쿼리와 같은 수준으로 그룹핑 되기 때문에 주의가 필요합니다.

    $user->posts()
            ->where('active', 1)
            ->orWhere('votes', '>=', 100)
            ->get();

The example above will generate the following SQL. As you can see, the `or` clause instructs the query to return _any_ user with greater than 100 votes. The query is no longer constrained to a specific user:

위의 코드는 아래와 같은 SQL을 생성합니다. 보시다시피 `or` 절은 100개 이상의 투표를 가진 포스트를 반환하도록 쿼리를 실행합니다. 연관관계를 통해서 의도한대로 특정 사용자가 제한되지 않습니다.  

```sql
select *
from posts
where user_id = ? and active = 1 or votes >= 100
```

In most situations, you should use [logical groups](/docs/{{version}}/queries#logical-grouping) to group the conditional checks between parentheses:

이런 경우에 대응해서 [논리 그룹](/docs/{{version}}/queries#logical-grouping)을 사용하여 괄호 사이에 조건을 추가하도록 그룹핑 해야합니다.

    use Illuminate\Database\Eloquent\Builder;

    $user->posts()
            ->where(function (Builder $query) {
                return $query->where('active', 1)
                             ->orWhere('votes', '>=', 100);
            })
            ->get();

The example above will produce the following SQL. Note that the logical grouping has properly grouped the constraints and the query remains constrained to a specific user:

위의 코드는 아래와 같은 SQL을 생성합니다. 논리 그룹기능을 사용하면 제약조건을 적절하게 그룹으로 묶어 연관관계를 위한 사용자 제한이 정상적으로 확인됩니다. 

```sql
select *
from posts
where user_id = ? and (active = 1 or votes >= 100)
```

<a name="relationship-methods-vs-dynamic-properties"></a>
### Relationship Methods Vs. Dynamic Properties
### 연관관계 메서드 Vs. 동적 속성

If you do not need to add additional constraints to an Eloquent relationship query, you may access the relationship as if it were a property. For example, continuing to use our `User` and `Post` example models, we may access all of a user's posts like so:

엘로퀀트 연관관계 쿼리에 제한을 추가할 필요가 없다면 이를 마치 속성처럼 사용하여 연관관계 모델에 접근할 수 있습니다. 예를 들어, `User`와 `Post` 예시 모델들을 계속해서 사용하면 다음과 같이 사용자의 모든 게시물에 접근할 수 있습니다.

    use App\Models\User;

    $user = User::find(1);

    foreach ($user->posts as $post) {
        // ...
    }

Dynamic relationship properties perform "lazy loading", meaning they will only load their relationship data when you actually access them. Because of this, developers often use [eager loading](#eager-loading) to pre-load relationships they know will be accessed after loading the model. Eager loading provides a significant reduction in SQL queries that must be executed to load a model's relations.

동적 연관관계 속성은 "지연 로딩"을 실행하므로, 실제로 연관관계에 접근 할 때 연관관계 데이터를 로드합니다. 그렇게 때문에 개발자들은 종종 모델을 로드한 뒤 접근해야할 연관관계들을 미리 로드해주는 [eager 로딩](#eager-loading)을 사용합니다. Eager 로딩은 모델의 연관관계를 로드하기 위해 실행되어야 할 SQL 쿼리 횟수를 효과적으로 줄여줍니다.

<a name="querying-relationship-existence"></a>
### Querying Relationship Existence
### 연관관계의 존재 확인 쿼리 질의하기

When retrieving model records, you may wish to limit your results based on the existence of a relationship. For example, imagine you want to retrieve all blog posts that have at least one comment. To do so, you may pass the name of the relationship to the `has` and `orHas` methods:

모델 데이터레코드를 조회할 때, 연관관계 모델이 존재하는지에 따라 쿼리 실행 결과를 제한하기 원할 수 있습니다. 예를 들어 하나 이상의 댓글을 가진 모든 블로그 게시물을 조회하려고 한다고 생각해 봅시다. 이를 위해서 `has` 또는 `orHas` 메서드로 연관관계의 이름을 전달하면 됩니다.

    use App\Models\Post;

    // Retrieve all posts that have at least one comment...
    $posts = Post::has('comments')->get();

You may also specify an operator and count value to further customize the query:

이 메서드에는 연관관계 조회를 위한 연산자와 카운트 수를 지정할 수도 있습니다. 

    // Retrieve all posts that have three or more comments...
    $posts = Post::has('comments', '>=', 3)->get();

Nested `has` statements may be constructed using "dot" notation. For example, you may retrieve all posts that have at least one comment that has at least one image:

중첩된 연관관계를 가지고 있다면 "점(.)" 표기법을 사용할 수 있습니다. 예를 들어 다음과 같이 이미지를 가지고 있는 댓글을 한 개 이상 가지고 있는 게시물을 조회할 수 있습니다. 

    // Retrieve posts that have at least one comment with images...
    $posts = Post::has('comments.images')->get();

If you need even more power, you may use the `whereHas` and `orWhereHas` methods to define additional query constraints on your `has` queries, such as inspecting the content of a comment:

더 많은 기능이 필요하다면, `has` 쿼리에 `whereHas`과 `orWhereHas` 메서드를 사용하여 댓글을 구분하기 위한 추가적인 쿼리 제약을 정의할 수 있습니다.  

    use Illuminate\Database\Eloquent\Builder;

    // Retrieve posts with at least one comment containing words like code%...
    $posts = Post::whereHas('comments', function (Builder $query) {
        $query->where('content', 'like', 'code%');
    })->get();

    // Retrieve posts with at least ten comments containing words like code%...
    $posts = Post::whereHas('comments', function (Builder $query) {
        $query->where('content', 'like', 'code%');
    }, '>=', 10)->get();

> **Warning**
> Eloquent does not currently support querying for relationship existence across databases. The relationships must exist within the same database.

> **Warning**
> 엘로퀀트는 다른 데이터베이스간의 존재 유무를 판단하는 기능을 지원하지 않습니다. 연관관계의 존재를 확인하는 쿼리를 수행하려면 연관관계가 동일한 데이터베이스 안에 있어야 합니다. 

<a name="inline-relationship-existence-queries"></a>
#### Inline Relationship Existence Queries
#### 인라인 연관관계의 존재 확인 쿼리 질의하기

If you would like to query for a relationship's existence with a single, simple where condition attached to the relationship query, you may find it more convenient to use the `whereRelation`, `orWhereRelation`, `whereMorphRelation`, and `orWhereMorphRelation` methods. For example, we may query for all posts that have unapproved comments:

연관관계 쿼리에 간단하게 연관관계 존재 확인만을 위한 조건을 추가하려는 경우에는 `whereRelation`, `orWhereRelation`, `whereMorphRelation`, `orWhereMorphRelation` 메서드를 사용하는 것이 더 편리할 수 있습니다. 예를 들어 승인되지 않은 댓글을 가지는 모든 포스트를 조회할 수 있습니다.

    use App\Models\Post;

    $posts = Post::whereRelation('comments', 'is_approved', false)->get();

Of course, like calls to the query builder's `where` method, you may also specify an operator:

이 경우에도 쿼리빌더의 `where` 메서드 호출과 마찬가지로, 연산자를 지정할 수 있습니다. 

    $posts = Post::whereRelation(
        'comments', 'created_at', '>=', now()->subHour()
    )->get();

<a name="querying-relationship-absence"></a>
### Querying Relationship Absence
### 연관관계된 모델이 존재하지 않는 것을 확인하며 질의하기

When retrieving model records, you may wish to limit your results based on the absence of a relationship. For example, imagine you want to retrieve all blog posts that **don't** have any comments. To do so, you may pass the name of the relationship to the `doesntHave` and `orDoesntHave` methods:

모델 데이터레코드를 조회할 때, 연관관계된 모델이 존재하지 않는 것에 따라서 결과를 제한하고자 할 수 있습니다. 예를 들어 코멘트를 가지고 있지 **않은** 모든 블로그 포스트를 조회하는 경우를 생각해 보겠습니다. 이렇게 하기 위해서는 `doesntHave` 또는 `orDoesntHave` 메서드에 정의한 연관관계의 이름을 전달하면됩니다.

    use App\Models\Post;

    $posts = Post::doesntHave('comments')->get();

If you need even more power, you may use the `whereDoesntHave` and `orWhereDoesntHave` methods to add additional query constraints to your `doesntHave` queries, such as inspecting the content of a comment:

더 많은 기능이 필요하다면, `doesntHave` 쿼리에 `whereDoesntHave` 와 `orWhereDoesntHave` 메서드를 사용하여 댓글을 구분하기 위한 추가적인 쿼리제약을 정의할 수 있습니다. 

    use Illuminate\Database\Eloquent\Builder;

    $posts = Post::whereDoesntHave('comments', function (Builder $query) {
        $query->where('content', 'like', 'code%');
    })->get();

You may use "dot" notation to execute a query against a nested relationship. For example, the following query will retrieve all posts that do not have comments; however, posts that have comments from authors that are not banned will be included in the results:

중첩된 연관관계에 대해서는 "점(.)" 표기법을 사용하여 쿼리를 질의할 수 있습니다. 예를 들어, 다음 쿼리는 댓글이 없는 모든 포스트를 조회합니다. 하지만 차단되지 않은 작성자의 댓글이 있는 게시물은 결과에 포함됩니다. 

    use Illuminate\Database\Eloquent\Builder;

    $posts = Post::whereDoesntHave('comments.author', function (Builder $query) {
        $query->where('banned', 0);
    })->get();

<a name="querying-morph-to-relationships"></a>
### Querying Morph To Relationships
### 다형성 연관관계 쿼리 질의하기

To query the existence of "morph to" relationships, you may use the `whereHasMorph` and `whereDoesntHaveMorph` methods. These methods accept the name of the relationship as their first argument. Next, the methods accept the names of the related models that you wish to include in the query. Finally, you may provide a closure which customizes the relationship query:

"morph to"(다형성) 연관관계가 존재하는지 확인하는 쿼리를 질의하기 위해서는 `whereHasMorph`와 `whereDoesntHaveMorph` 메서드를 사용할 수 있습니다. 이 메서드는 첫번째 인자로 연관관계의 이름을 전달받고, 쿼리 결과에 포함하고자 하는 관련 모델의 이름을 두 번째 인자로 전달받습니다. 세번째 인자는 연관관계 쿼리를 커스터마이징 할 수 있는 클로저를 전달 받을 수 있습니다.  

    use App\Models\Comment;
    use App\Models\Post;
    use App\Models\Video;
    use Illuminate\Database\Eloquent\Builder;

    // Retrieve comments associated to posts or videos with a title like code%...
    $comments = Comment::whereHasMorph(
        'commentable',
        [Post::class, Video::class],
        function (Builder $query) {
            $query->where('title', 'like', 'code%');
        }
    )->get();

    // Retrieve comments associated to posts with a title not like code%...
    $comments = Comment::whereDoesntHaveMorph(
        'commentable',
        Post::class,
        function (Builder $query) {
            $query->where('title', 'like', 'code%');
        }
    )->get();

You may occasionally need to add query constraints based on the "type" of the related polymorphic model. The closure passed to the `whereHasMorph` method may receive a `$type` value as its second argument. This argument allows you to inspect the "type" of the query that is being built:

관련된 모델이 어떤 "타입" 이냐에 따라서 다른 제약조건을 추가해야할 수도 있기 때문에, `whereHasMorph` 메서드에 전달되는 클로저에는 두번째 인자로 `$type`을 받을 수 있습니다. 이 인자 통해서 작성중인 쿼리의 "타입"을 확인할수 있습니다.     

    use Illuminate\Database\Eloquent\Builder;

    $comments = Comment::whereHasMorph(
        'commentable',
        [Post::class, Video::class],
        function (Builder $query, string $type) {
            $column = $type === Post::class ? 'content' : 'title';

            $query->where($column, 'like', 'code%');
        }
    )->get();

<a name="querying-all-morph-to-related-models"></a>
#### Querying All Related Models
#### 모든 관련된 모델에 대한 쿼리 질의하기

Instead of passing an array of possible polymorphic models, you may provide `*` as a wildcard value. This will instruct Laravel to retrieve all of the possible polymorphic types from the database. Laravel will execute an additional query in order to perform this operation:

다형성 연관관계에 대한 쿼리를 질의할 때 대상으로할 다형성 모델배열을 전달하는 대신에 `*` 형식의 와일드카드 값을 전달할 수 있습니다. 이렇게하면 라라벨이 데이터베이스에서 가능한 모든 다형성 타입을 조회하게 됩니다. 라라벨은 이 작업을 수행하기 위한 추가 쿼리를 실행합니다.

    use Illuminate\Database\Eloquent\Builder;

    $comments = Comment::whereHasMorph('commentable', '*', function (Builder $query) {
        $query->where('title', 'like', 'foo%');
    })->get();

<a name="aggregating-related-models"></a>
## Aggregating Related Models
## 관련 모델들 집계하기

<a name="counting-related-models"></a>
### Counting Related Models
### 연관된 모델의 개수 확인하기-카운팅

Sometimes you may want to count the number of related models for a given relationship without actually loading the models. To accomplish this, you may use the `withCount` method. The `withCount` method will place a `{relation}_count` attribute on the resulting models:

때로는, 연관관계 모델 데이터를 로드하지 않고 주어진 연관관계 모델의 갯수만 알고 싶을 수 있습니다. 이런 경우에는 `withCount` 메서드를 사용할 수 있습니다. `withCount` 메서드는 쿼리 실행 결과에 `{relation}_count` 속성을 조회할 수 있게 합니다. 

    use App\Models\Post;

    $posts = Post::withCount('comments')->get();

    foreach ($posts as $post) {
        echo $post->comments_count;
    }

By passing an array to the `withCount` method, you may add the "counts" for multiple relations as well as add additional constraints to the queries:

`withCount` 메서드에 배열을 전달하면 여러개의 연관관계 모델에 대한 "갯수"를 확인할 수 있습니다. 또한 쿼리에 제약조건을 추가할 수 있습니다. 

    use Illuminate\Database\Eloquent\Builder;

    $posts = Post::withCount(['votes', 'comments' => function (Builder $query) {
        $query->where('content', 'like', 'code%');
    }])->get();

    echo $posts[0]->votes_count;
    echo $posts[0]->comments_count;

You may also alias the relationship count result, allowing multiple counts on the same relationship:

동일한 연관관계에 대하여 여러번 카운트를 수행하기 위해서 카운트 결과에 별칭(alias)를 부여할 수도 있습니다.

    use Illuminate\Database\Eloquent\Builder;

    $posts = Post::withCount([
        'comments',
        'comments as pending_comments_count' => function (Builder $query) {
            $query->where('approved', false);
        },
    ])->get();

    echo $posts[0]->comments_count;
    echo $posts[0]->pending_comments_count;

<a name="deferred-count-loading"></a>
#### Deferred Count Loading
#### 카운트 로딩 지연

Using the `loadCount` method, you may load a relationship count after the parent model has already been retrieved:

`loadCount` 메서드를 사용하면 상위 모델이 조회된 이후 연관관계 카운트를 로드할 수 있습니다.

    $book = Book::first();

    $book->loadCount('genres');

If you need to set additional query constraints on the count query, you may pass an array keyed by the relationships you wish to count. The array values should be closures which receive the query builder instance:

카운트 쿼리에 대한 추가적인 제약조건을 지정하려는 경우 카운트하려는 연관관계가 키로 지정된 배열을 전달하면 됩니다. 배열의 값은 쿼리 빌더 인스턴스를 인자로 받는 클로저여야 합니다. 

    $book->loadCount(['reviews' => function (Builder $query) {
        $query->where('rating', 5);
    }])

<a name="relationship-counting-and-custom-select-statements"></a>
#### Relationship Counting & Custom Select Statements
#### 연관관게 카운팅 & 조회 구문 결합 

If you're combining `withCount` with a `select` statement, ensure that you call `withCount` after the `select` method:

`withCount` 와 `select` 구문을 조합해서 사용한다면, `select` 메서드 뒤에 `withCount` 메서드를 호출하도록 코드를 작성하십시오.

    $posts = Post::select(['title', 'body'])
                    ->withCount('comments')
                    ->get();

<a name="other-aggregate-functions"></a>
### Other Aggregate Functions
### 기타 집계 기능

In addition to the `withCount` method, Eloquent provides `withMin`, `withMax`, `withAvg`, `withSum`, and `withExists` methods. These methods will place a `{relation}_{function}_{column}` attribute on your resulting models:

`withCount` 메서드에 더해서, 엘로퀀트는 `withMin`, `withMax`, `withAvg`, `withSum`, `withExists` 메서드를 제공합니다. 이 메서드들은 쿼리 결과에 `{relation}_{function}_{column}` 속성을 조회할 수 있도록 합니다. 

    use App\Models\Post;

    $posts = Post::withSum('comments', 'votes')->get();

    foreach ($posts as $post) {
        echo $post->comments_sum_votes;
    }

If you wish to access the result of the aggregate function using another name, you may specify your own alias:

집계 기능의 결과 항목을 다른이름으로 지정하고자 한다면 다음과 같이 별칭을 부여할 수 있습니다.

    $posts = Post::withSum('comments as total_comments', 'votes')->get();

    foreach ($posts as $post) {
        echo $post->total_comments;
    }

Like the `loadCount` method, deferred versions of these methods are also available. These additional aggregate operations may be performed on Eloquent models that have already been retrieved:

`loadCount` 메서드와 마찬가지로 이러한 메서드의 지연된 버전도 사용할 수 있습니다. 이미 검색된 엘로퀀트 모델에서 다음과 같은 추가적인 집계 작업을 수행할 수 있습니다.

    $post = Post::first();

    $post->loadSum('comments', 'votes');

If you're combining these aggregate methods with a `select` statement, ensure that you call the aggregate methods after the `select` method:

이러한 집계 메서드와 `select` 구문을 조합해서 사용한다면, `select` 메서드 뒤에 집계 메서드를 호출하도록 코드를 작성하십시오.

    $posts = Post::select(['title', 'body'])
                    ->withExists('comments')
                    ->get();


<a name="counting-related-models-on-morph-to-relationships"></a>
### Counting Related Models On Morph To Relationships
### 다형성 연관관계에서 관련된 모델 카운트 확인하기

If you would like to eager load a "morph to" relationship, as well as related model counts for the various entities that may be returned by that relationship, you may utilize the `with` method in combination with the `morphTo` relationship's `morphWithCount` method.

"morph to" 연관관계 및 해당 연관관계에 의해 반환될 수 있는 다양한 엔터티에 관련 모델의 카운트를 수를 eager 로드하려면 `with` 메서드 안에서 `morphTo` 메서드와 `morphWithCount` 메서드를 조합하여 사용하면 됩니다.

In this example, let's assume that `Photo` and `Post` models may create `ActivityFeed` models. We will assume the `ActivityFeed` model defines a "morph to" relationship named `parentable` that allows us to retrieve the parent `Photo` or `Post` model for a given `ActivityFeed` instance. Additionally, let's assume that `Photo` models "have many" `Tag` models and `Post` models "have many" `Comment` models.

이 예시에서 `Photo` 및 `Post` 모델이 `ActivityFeed` 모델을 생성할 수 있다고 가정해 보겠습니다. 우리는 `ActivityFeed` 모델이 `parentable`이라는 이름의 "morph to" 다형성 연관관계를 정의하여 주어진 `ActivityFeed` 인스턴스에 대한 상위 모델로 `Photo` 또는 `Post`을 검색할 수 있다고 가정하겠습니다. 또한, `Photo` 모델은 `Tag` 모델을 "많이(일대다)" 가지고 있고, `Post` 모델은 `Comment` 모델을 "많이(일대다)" 가지고 있다고 가정해 보겠습니다.

Now, let's imagine we want to retrieve `ActivityFeed` instances and eager load the `parentable` parent models for each `ActivityFeed` instance. In addition, we want to retrieve the number of tags that are associated with each parent photo and the number of comments that are associated with each parent post:

이제 `ActivityFeed` 인스턴스를 조회하여 각 `ActivityFeed` 인스턴스에 대해 `parentable` 연관관계의 상위 모델을 eager 로드한다고 가정해 보겠습니다. 이에 더해 상위 모델인 사진에 연결된 태그 수와 상위 모델인 게시물과 연결된 댓글 수를 조회한다고 해보겠습니다.

    use Illuminate\Database\Eloquent\Relations\MorphTo;

    $activities = ActivityFeed::with([
        'parentable' => function (MorphTo $morphTo) {
            $morphTo->morphWithCount([
                Photo::class => ['tags'],
                Post::class => ['comments'],
            ]);
        }])->get();

<a name="morph-to-deferred-count-loading"></a>
#### Deferred Count Loading
#### 지연된 카운트 로딩

Let's assume we have already retrieved a set of `ActivityFeed` models and now we would like to load the nested relationship counts for the various `parentable` models associated with the activity feeds. You may use the `loadMorphCount` method to accomplish this:

`ActivityFeed` 모델의 인스턴스들을 이미 조회한 뒤에 활동 피드(activity feeds)와 연결된 다양한 `parentable` 모델에 대한 중첩된 연관관계 카운트 수를 구한다고 가정해보겠습니다. 이를 위해서는 `loadMorphCount` 메서드를 사용할 수 있습니다.

    $activities = ActivityFeed::with('parentable')->get();

    $activities->loadMorphCount('parentable', [
        Photo::class => ['tags'],
        Post::class => ['comments'],
    ]);

<a name="eager-loading"></a>
## Eager Loading
## Eager 로딩

When accessing Eloquent relationships as properties, the related models are "lazy loaded". This means the relationship data is not actually loaded until you first access the property. However, Eloquent can "eager load" relationships at the time you query the parent model. Eager loading alleviates the "N + 1" query problem. To illustrate the N + 1 query problem, consider a `Book` model that "belongs to" to an `Author` model:

엘로퀀트 연관관계들을 속성으로 접근할 때 연관관계 데이터는 "지연 로드" 됩니다. 이는 실제로 속성에 엑세스 하기 전까지 연관관계 데이터가 로드되지 않는다는 것을 의미합니다. 하지만 엘로퀀트는 상위 모델을 조회할 때 연관관계를 맺고 있는 하위 모델을 "eager 로드-즉시로드"할 수있도록 기능을 제공합니다. Eager 로딩은 N + 1 쿼리 문제를 해결 합니다. N + 1 쿼리 문제에 대한 예제를 들어보자면 `Author`에 "소속되어 있는(일대다)" `Book` 모델을 생각해보겠습니다.

    <?php

    namespace App\Models;

    use Illuminate\Database\Eloquent\Model;
    use Illuminate\Database\Eloquent\Relations\BelongsTo;

    class Book extends Model
    {
        /**
         * Get the author that wrote the book.
         */
        public function author(): BelongsTo
        {
            return $this->belongsTo(Author::class);
        }
    }

Now, let's retrieve all books and their authors:

이제 모든 책과 그 저자들을 조회해봅시다.

    use App\Models\Book;

    $books = Book::all();

    foreach ($books as $book) {
        echo $book->author->name;
    }

This loop will execute one query to retrieve all of the books within the database table, then another query for each book in order to retrieve the book's author. So, if we have 25 books, the code above would run 26 queries: one for the original book, and 25 additional queries to retrieve the author of each book.

이 반복문은 테이블에서 모든 책들을 조회하는 한번의 쿼리를 실행하고, 각각의 책마다 저자를 조회하는 각각의 쿼리를 실행할 것입니다. 따라서, 만약 25개의 책이 있다면, 위의 코드는 총 26개의 쿼리를 실행하게 됩니다. 책목록을 조회하기 위한 한번의 쿼리와 각 책의 저자를 조회하는 25개의 추가적인 쿼리를 실행합니다.

Thankfully, we can use eager loading to reduce this operation to just two queries. When building a query, you may specify which relationships should be eager loaded using the `with` method:

다행히도, eager 로딩을 사용하면 이 작업을 두개의 쿼리로 줄일 수 있습니다. 쿼리를 실행할 때 `with` 메서드를 사용하여 어떤 연관관계가 eager 로드되어야 하는지 지정할 수 있습니다.

    $books = Book::with('author')->get();

    foreach ($books as $book) {
        echo $book->author->name;
    }

For this operation, only two queries will be executed - one query to retrieve all of the books and one query to retrieve all of the authors for all of the books:

이 작업에서는 두 개의 쿼리가 실행될 것입니다. 첫 번째 쿼리는 전체 책을 조회하는 쿼리이고, 두 번째 쿼리는 조회된 책의 저자를 조회하기 위한 쿼리입니다.

```sql
select * from books

select * from authors where id in (1, 2, 3, 4, 5, ...)
```

<a name="eager-loading-multiple-relationships"></a>
#### Eager Loading Multiple Relationships
#### 여러 연관관계에 대해서 Eager 로딩하기

Sometimes you may need to eager load several different relationships. To do so, just pass an array of relationships to the `with` method:

종종 여러 개의 다른 연관관계들을 eager 로드해야 될 때가 있습니다. 이 경우 `with` 메서드에 연관관계 배열을 전달하면 됩니다.

    $books = Book::with(['author', 'publisher'])->get();

<a name="nested-eager-loading"></a>
#### Nested Eager Loading
#### 중첩된 Eager 로딩하기

To eager load a relationship's relationships, you may use "dot" syntax. For example, let's eager load all of the book's authors and all of the author's personal contacts:

"점" 구문을 이용하면 연관관계의 연관관계(중첩된 연관관계)를 eager 로드할 수 있습니다. 예를 들어, 책의 모든 저자들과 저자들의 모든 연락처를 eager 로드해보겠습니다.

    $books = Book::with('author.contacts')->get();

Alternatively, you may specify nested eager loaded relationships by providing a nested array to the `with` method, which can be convenient when eager loading multiple nested relationships:

또다른 방법으로, 중첩 배열로 `with` 메서드에 제공하는 방식으로 중첩된 이거 로드 관계를 지정할 수 있습니다. 여러 중첩된 관계를 이거 로드할 때 편리하게 쓸 수 있습니다.

    $books = Book::with([
        'author' => [
            'contacts',
            'publisher',
        ],
    ])->get();

<a name="nested-eager-loading-morphto-relationships"></a>
#### Nested Eager Loading `morphTo` Relationships
#### 중첩 된 `morphTo` 연관관계의 Eager 로딩

If you would like to eager load a `morphTo` relationship, as well as nested relationships on the various entities that may be returned by that relationship, you may use the `with` method in combination with the `morphTo` relationship's `morphWith` method. To help illustrate this method, let's consider the following model:

`morphTo` 연관관계뿐만 아니라 그 연관관계에 의해 반환 될 수 있는 다양한 엔티티들에 중첩된 연관관계를 eager 로드 하고 싶다면, `with` 메서드 안에서 `morph` 연관관계의 `morphWith` 메서드를 조합하여 사용하면 됩니다. 이 방법을 설명하기 위해 다음 모델을 고려해보겠습니다.

    <?php

    use Illuminate\Database\Eloquent\Model;
    use Illuminate\Database\Eloquent\Relations\MorphTo;

    class ActivityFeed extends Model
    {
        /**
         * Get the parent of the activity feed record.
         */
        public function parentable(): MorphTo
        {
            return $this->morphTo();
        }
    }

In this example, let's assume `Event`, `Photo`, and `Post` models may create `ActivityFeed` models. Additionally, let's assume that `Event` models belong to a `Calendar` model, `Photo` models are associated with `Tag` models, and `Post` models belong to an `Author` model.

이 예제에서 `Event`,`Photo`,`Post` 모델이 `ActivityFeed` 모델을 생성한다고 가정해보겠습니다. 그리고 `Event`모델이 `Calendar`모델에 소속되어 있고, `Photo`모델이 `Tag` 모델과 관련이 있고 `Post` 모델이 `Author` 모델에 소속되어 있다고 가정 해 보겠습니다. (Calendar:Event - 1:N, Photo:Tag - N:M, Author:Post - 1:N)

Using these model definitions and relationships, we may retrieve `ActivityFeed` model instances and eager load all `parentable` models and their respective nested relationships:

이 모델 정의와 연관관계를 사용하면 `ActivityFeed` 모델 인스턴스를 조회 하면서 모든 `parentable` 모델과 각각의 중첩된 연관관계를 eager 로드 할 수 있습니다.

    use Illuminate\Database\Eloquent\Relations\MorphTo;

    $activities = ActivityFeed::query()
        ->with(['parentable' => function (MorphTo $morphTo) {
            $morphTo->morphWith([
                Event::class => ['calendar'],
                Photo::class => ['tags'],
                Post::class => ['author'],
            ]);
        }])->get();

(역자주: ActivityFeed 가 다양한 모델(Event, Photo, Post)와 다형성 연관관계를 가지고 있고 각각의 연관관계에 있는 모델(Event, Photo, Post)이 다시 연관관계를 형성하고 있을 때 ActivityFeed를 조회하면서 다형성 연관관계와 관련된 연관관계를 Eager 로딩하는 복잡한 예시입니다.)

<a name="eager-loading-specific-columns"></a>
#### Eager Loading Specific Columns
#### Eager 로딩에서 컬럼 지정하기

You may not always need every column from the relationships you are retrieving. For this reason, Eloquent allows you to specify which columns of the relationship you would like to retrieve:

Eager 로딩에서 조회하고자 하는 연관관계 모델의 모든 컬럼이 항상 필요한 것은 아닙니다. 특정 컬럼만을 로딩하고자 한다면 조회하고자 하는 연관관계에 컬럼을 지정할 수 있습니다.

    $books = Book::with('author:id,name,book_id')->get();

> **Warning**
> When using this feature, you should always include the `id` column and any relevant foreign key columns in the list of columns you wish to retrieve.

> **Warning**
> 이 기능을 사용할 때에는, 조회하고자 하는 컬럼에 항상 `id` 컬럼과 관련 외래 키 컬럼이 포함되어 있어야 합니다.

<a name="eager-loading-by-default"></a>
#### Eager Loading By Default
#### 모델을 로딩할 때 연관관계모델을 항상 Eager 로딩 하기

Sometimes you might want to always load some relationships when retrieving a model. To accomplish this, you may define a `$with` property on the model:

때로는 모델을 조회 할 때 연관관계에 있는 모델을 항상 로드해서 사용할 수 있습니다. 이런 경우에는 모델의 `$with` 속성을 정의하면 됩니다.

    <?php

    namespace App\Models;

    use Illuminate\Database\Eloquent\Model;
    use Illuminate\Database\Eloquent\Relations\BelongsTo;

    class Book extends Model
    {
        /**
         * The relationships that should always be loaded.
         *
         * @var array
         */
        protected $with = ['author'];

        /**
         * Get the author that wrote the book.
         */
        public function author(): BelongsTo
        {
            return $this->belongsTo(Author::class);
        }

        /**
         * Get the genre of the book.
         */
        public function genre(): BelongsTo
        {
            return $this->belongsTo(Genre::class);
        }
    }

If you would like to remove an item from the `$with` property for a single query, you may use the `without` method:

쿼리를 실행할 때 `$with` 속성의 값을 무시하려면 `without` 메서드를 사용할 수 있습니다.

    $books = Book::without('author')->get();

If you would like to override all items within the `$with` property for a single query, you may use the `withOnly` method:

쿼리를 실행할 때 `$with` 속성의 모든 항목을 재지정하려면 `withOnly` 메서드를 사용하면 됩니다.

    $books = Book::withOnly('genre')->get();

<a name="constraining-eager-loads"></a>
### Constraining Eager Loads
### Eager 로딩에서 제약 조건을 추가하기

Sometimes you may wish to eager load a relationship but also specify additional query conditions for the eager loading query. You can accomplish this by passing an array of relationships to the `with` method where the array key is a relationship name and the array value is a closure that adds additional constraints to the eager loading query:

연관관계 모델을 Eager 로드하고 싶지만 로딩할 때 추가적인 쿼리 제약조건을 지정할 수 있습니다. `with` 메서드에 인자로 전달하는 값은 배열의 키는 연관관계의 이름이되고 배열의 값은 Eager 로딩 쿼리에 제약조건을 추가할 클로저로 이루어져 있습니다. 

    use App\Models\User;

    $users = User::with(['posts' => function (Builder $query) {
        $query->where('title', 'like', '%code%');
    }])->get();

In this example, Eloquent will only eager load posts where the post's `title` column contains the word `code`. You may call other [query builder](/docs/{{version}}/queries) methods to further customize the eager loading operation:

이 예제에서 엘로퀀트는 포스트의 `title` 컬럼이 `code`라는 단어를 포함할 때만 게시물을 eager 로드할 것입니다. 다른 [쿼리 빌더](/docs/{{version}}/queries)메서드를 호출하여 계속하여서 eager 로딩 작업을 커스터마이즈할 수 있습니다.

    $users = User::with(['posts' => function (Builder $query) {
        $query->orderBy('created_at', 'desc');
    }])->get();

> **Warning**
> The `limit` and `take` query builder methods may not be used when constraining eager loads.

> **Warning**
> eager 로드에 제약조건을 추가할 때에는 `limit`과 `take` 쿼리 빌더 메서드는 사용할 수 없습니다.

<a name="constraining-eager-loading-of-morph-to-relationships"></a>
#### Constraining Eager Loading Of `morphTo` Relationships
#### `morphTo` 연관관계에서의 Eager 로딩 제약조건 추가하기

If you are eager loading a `morphTo` relationship, Eloquent will run multiple queries to fetch each type of related model. You may add additional constraints to each of these queries using the `MorphTo` relation's `constrain` method:

`morphTo` 연관관계에서 Eager 로딩을 수행할 때 엘로퀀트는 연관된 모델을 위해서 여러번 쿼리를 수행합니다. `MorphTo` 연관관계의 `constrain` 메서드를 사용하면 각각 타입에 대한 구분된 추가 제약조건 쿼리를 지정할 수 있습니다.

    use Illuminate\Database\Eloquent\Builder;
    use Illuminate\Database\Eloquent\Relations\MorphTo;

    $comments = Comment::with(['commentable' => function (MorphTo $morphTo) {
        $morphTo->constrain([
            Post::class => function (Builder $query) {
                $query->whereNull('hidden_at');
            },
            Video::class => function (Builder $query) {
                $query->where('type', 'educational');
            },
        ]);
    }])->get();

In this example, Eloquent will only eager load posts that have not been hidden and videos that have a `type` value of "educational".

위 예시에서 엘로퀀트는 숨김상태가 아닌 포스트와, `type` 값이 "educational" 인 비디오 모델을 Eager 로딩합니다. 

<a name="constraining-eager-loads-with-relationship-existence"></a>
#### Constraining Eager Loads With Relationship Existence
#### 관계가 있는 상태에서 이거 로드 제한

You may sometimes find yourself needing to check for the existence of a relationship while simultaneously loading the relationship based on the same conditions. For example, you may wish to only retrieve `User` models that have child `Post` models matching a given query condition while also eager loading the matching posts. You may accomplish this using the `withWhereHas` method:

동일한 조건을 기반으로 관계를 로드하는 동시에 관계의 존재를 확인해야 하는 경우가 있습니다. 예를 들어, 주어진 쿼리 조건과 일치하면서 `Post` 모델을 자식으로 가지고 있는 `User` 모델만 검색하는 동시에 매칭된 포스트를 즉시 로드하길 원할 수 있습니다. `withWhereHas` 메서드를 사용하여 이 작업을 수행할 수 있습니다.

    use App\Models\User;
    use Illuminate\Database\Eloquent\Builder;

    $users = User::withWhereHas('posts', function (Builder $query) {
        $query->where('featured', true);
    })->get();

<a name="lazy-eager-loading"></a>
### Lazy Eager Loading
### 지연 Eager 로딩

Sometimes you may need to eager load a relationship after the parent model has already been retrieved. For example, this may be useful if you need to dynamically decide whether to load related models:

때로는 부모 모델을 조회한 뒤에 연관관계를 eager 로드해야할 수 있습니다. 예를 들어, 연관된 모델들을 로딩해야할지 여부를 동적으로 결정해야할 때 유용하게 사용됩니다.

    use App\Models\Book;

    $books = Book::all();

    if ($someCondition) {
        $books->load('author', 'publisher');
    }

If you need to set additional query constraints on the eager loading query, you may pass an array keyed by the relationships you wish to load. The array values should be closure instances which receive the query instance:

Eager 로딩 쿼리에 추가적인 쿼리 제한을 지정해야 할 경우, `load` 메서드에 로그하고자 하는 연관관계에 대한 키로 이루어진 배열을 전달할 수 있습니다. 이 배열의 값은 쿼리 인스턴스를 인자로 받아들이는 클로저여야만 합니다.

    $author->load(['books' => function (Builder $query) {
        $query->orderBy('published_date', 'asc');
    }]);

To load a relationship only when it has not already been loaded, use the `loadMissing` method:

로딩되어 있지 않았을 때에만 연관관계 모델을 로딩하려면 `loadMissing` 메서드를 사용하면됩니다.

    $book->loadMissing('author');

<a name="nested-lazy-eager-loading-morphto"></a>
#### Nested Lazy Eager Loading & `morphTo`
#### 중첩된 지연 Eager 로딩 & `morphTo`

If you would like to eager load a `morphTo` relationship, as well as nested relationships on the various entities that may be returned by that relationship, you may use the `loadMorph` method.

`morphTo` 연관관계 뿐만 아니라 해당 연관관계에 의해 반환될 수 있는 다양한 엔티티에서의 중첩된 연관관계를 원하는 경우 `loadMorph` 메서드를 사용할 수 있습니다.

This method accepts the name of the `morphTo` relationship as its first argument, and an array of model / relationship pairs as its second argument. To help illustrate this method, let's consider the following model:

이 메서드는 첫번째 인자로 `morphTo` 연관관계를 사용하고 두번째 인자로 일련의 모델 / 짝지은 연관관계(relationship pairs)를 사용합니다. 이 메서드를 설명하기 위해 다음 모델을 살펴보겠습니다.

    <?php

    use Illuminate\Database\Eloquent\Model;
    use Illuminate\Database\Eloquent\Relations\MorphTo;

    class ActivityFeed extends Model
    {
        /**
         * Get the parent of the activity feed record.
         */
        public function parentable(): MorphTo
        {
            return $this->morphTo();
        }
    }

In this example, let's assume `Event`, `Photo`, and `Post` models may create `ActivityFeed` models. Additionally, let's assume that `Event` models belong to a `Calendar` model, `Photo` models are associated with `Tag` models, and `Post` models belong to an `Author` model.

이 예제에서는 `Event`, `Photo`, `Post` 모델이 `ActivityFeed` 모델을 만들 수 있다고 가정해보겠습니다. 또한 `Event` 모델은 `Calendar` 모델에 속하고 `Photo` 모델은 `Tag` 모델, `Post` 모델은 `Author` 모델에 속한다고 가정해보겠습니다.

Using these model definitions and relationships, we may retrieve `ActivityFeed` model instances and eager load all `parentable` models and their respective nested relationships:

이러한 모델 정의와 연관관계를 사용하여 `ActivityFeed` 모델 인스턴스를 조회하고 모든 `parentable` 모델과 각각 중첩된 연관관계를 eager 로드할 수 있습니다.

    $activities = ActivityFeed::with('parentable')
        ->get()
        ->loadMorph('parentable', [
            Event::class => ['calendar'],
            Photo::class => ['tags'],
            Post::class => ['author'],
        ]);

<a name="preventing-lazy-loading"></a>
### Preventing Lazy Loading
### 지연로딩 방지하기

As previously discussed, eager loading relationships can often provide significant performance benefits to your application. Therefore, if you would like, you may instruct Laravel to always prevent the lazy loading of relationships. To accomplish this, you may invoke the `preventLazyLoading` method offered by the base Eloquent model class. Typically, you should call this method within the `boot` method of your application's `AppServiceProvider` class.

앞서 이야기한 바와 같이 연관관계의 Eager 로딩은 애플리케이션에 상당한 성능의 이점을 제공할 수 있습니다. 그래서 때로는 연관관계의 지연로딩을 항상 방지하도록 애플리케이션을 설정할 수 있습니다. 이를 위해서는 엘로퀀트 기본 모델에서 제공하는 `preventLazyLoading` 메서드를 호출하면 됩니다. 메서드 호출은 일반적으로 애플리케이션의 `AppServiceProvider` 클래스의 `boot` 메서드에서 진행합니다. 

The `preventLazyLoading` method accepts an optional boolean argument that indicates if lazy loading should be prevented. For example, you may wish to only disable lazy loading in non-production environments so that your production environment will continue to function normally even if a lazy loaded relationship is accidentally present in production code:

`preventLazyLoading` 메서드는 지연 로딩을 방지할지 말지를 나타내는 boolean 값을 인자로 전달 받습니다. 예를 들어, 프로덕션 코드가 아닌 경우에만 지연로딩을 방지하려고 한다면 다음과 같이 코드를 정의하면 됩니다.

```php
use Illuminate\Database\Eloquent\Model;

/**
 * Bootstrap any application services.
 */
public function boot(): void
{
    Model::preventLazyLoading(! $this->app->isProduction());
}
```

After preventing lazy loading, Eloquent will throw a `Illuminate\Database\LazyLoadingViolationException` exception when your application attempts to lazy load any Eloquent relationship.

지연로딩 방지 기능을 적용하고 나면, 엘로퀀트는 연관관계를 지연로딩하려고 할 때마다 `Illuminate\Database\LazyLoadingViolationException` 예외를 발생시킵니다.

You may customize the behavior of lazy loading violations using the `handleLazyLoadingViolationsUsing` method. For example, using this method, you may instruct lazy loading violations to only be logged instead of interrupting the application's execution with exceptions:

`handleLazyLoadingViolationsUsing` 메소드를 사용하면 지연로딩 방지 위반이 발생했을 때 어떤 동작을 수행햐야하는지 커스터마이징 할 수 있습니다. 예를 들어, 예외를 발생시키는 대신 다음과 같이 지연 로드 방지 위반에 대한 로깅만 남도록 정의할 수 있습니다.

```php
Model::handleLazyLoadingViolationUsing(function (Model $model, string $relation) {
    $class = get_class($model);

    info("Attempted to lazy load [{$relation}] on model [{$class}].");
});
```

<a name="inserting-and-updating-related-models"></a>
## Inserting & Updating Related Models
## 연관된 모델 삽입하기 & 수정하기

<a name="the-save-method"></a>
### The `save` Method
### `Save` 메서드

Eloquent provides convenient methods for adding new models to relationships. For example, perhaps you need to add a new comment to a post. Instead of manually setting the `post_id` attribute on the `Comment` model you may insert the comment using the relationship's `save` method:

엘로퀀트는 연관관계에 새로운 모델을 추가하는 편리한 메서드들을 제공합니다. 예를 들어, `Post` 모델에 새로운 `Comment`를 추가해야 할 수 있습니다. `Comment` 모델에 수동으로 `post_id` 속성을 지정하는 대신 연관관계에 `save` 메서드를 사용해서 새로운 댓글을 추가할 수 있습니다.

    use App\Models\Comment;
    use App\Models\Post;

    $comment = new Comment(['message' => 'A new comment.']);

    $post = Post::find(1);

    $post->comments()->save($comment);

Note that we did not access the `comments` relationship as a dynamic property. Instead, we called the `comments` method to obtain an instance of the relationship. The `save` method will automatically add the appropriate `post_id` value to the new `Comment` model.

`comments` 연관관계를 동적 속성으로 접근하지 않았다는 점을 주목하십시오. 대신에 `comments` 메서드를 호출하여 연관관계의 인스턴스를 얻었습니다. `save` 메서드는 자동으로 새로운 `Comment` 모델에 적절한 `post_id` 값을 추가할 것입니다.

If you need to save multiple related models, you may use the `saveMany` method:

여러 개의 관련된 모델을 저장해야 한다면 `saveMany` 메서드를 사용하면됩니다.

    $post = Post::find(1);

    $post->comments()->saveMany([
        new Comment(['message' => 'A new comment.']),
        new Comment(['message' => 'Another new comment.']),
    ]);

The `save` and `saveMany` methods will persist the given model instances, but will not add the newly persisted models to any in-memory relationships that are already loaded onto the parent model. If you plan on accessing the relationship after using the `save` or `saveMany` methods, you may wish to use the `refresh` method to reload the model and its relationships:

`save` 및 `saveMany` 메서드는 인자로 전달된 모델 인스턴스를 저장하지만, 이미 로딩된 상위 모델과 저장한 모델사이의 연관관계를 메모리에 추가하지는 않습니다. 따라서 `save` 와 `saveMany` 메서드를 사용하여 연관모델을 저장한 뒤에 추가한 연관 모델을 연관관계를 통해서 조회하고자 한다면 상위 모델의 `refresh` 메서드를 호출하여 연관관계 모델을 다시 로딩할 수 있습니다. 

    $post->comments()->save($comment);

    $post->refresh();

    // All comments, including the newly saved comment...
    $post->comments;

<a name="the-push-method"></a>
#### Recursively Saving Models & Relationships
#### 재귀적으로 모델 및 연관관계 저장

If you would like to `save` your model and all of its associated relationships, you may use the `push` method. In this example, the `Post` model will be saved as well as its comments and the comment's authors:

모델과 관련된 모든 연관관계를 `save` 하고 싶다면 `push` 메서드를 사용할 수 있습니다. 다음 예제에서 `Post` 모델은 댓글과 댓글 작성자와 함께 저장됩니다.

    $post = Post::find(1);

    $post->comments[0]->message = 'Message';
    $post->comments[0]->author->name = 'Author Name';

    $post->push();

The `pushQuietly` method may be used to save a model and its associated relationships without raising any events:

`pushQuietly` 메서드는 이벤트를 발생시키지 않고 모델 및 관련 관계를 저장하는 데 사용할 수 있습니다.

    $post->pushQuietly();

<a name="the-create-method"></a>
### The `create` Method
### `create` 메서드

In addition to the `save` and `saveMany` methods, you may also use the `create` method, which accepts an array of attributes, creates a model, and inserts it into the database. The difference between `save` and `create` is that `save` accepts a full Eloquent model instance while `create` accepts a plain PHP `array`. The newly created model will be returned by the `create` method:

`save`와 `saveMany` 메서드 외에도 저장하려는 모델 속성을 배열을 인자로 해서 모델을 생성하고 데이터베이스에 저장하는 `create` 메서드를 사용할 수 있습니다. `save` 메서드와 `create` 메서드의 차이는 `save`는 엘로퀀트 모델 인스턴스를 인자로 받는 반면에 `create`는 순수 PHP `배열`를 받는다는 점에서 차이가 있습니다. `create` 메서드의 결과로 새로 생성된 모델이 반환됩니다.

    use App\Models\Post;

    $post = Post::find(1);

    $comment = $post->comments()->create([
        'message' => 'A new comment.',
    ]);

You may use the `createMany` method to create multiple related models:

`createMany` 메서드를 사용해서 여러 개의 관련된 모델을 생성(create) 할 수 있습니다.

    $post = Post::find(1);

    $post->comments()->createMany([
        ['message' => 'A new comment.'],
        ['message' => 'Another new comment.'],
    ]);

The `createQuietly` and `createManyQuietly` methods may be used to create a model(s) without dispatching any events:

`createQuietly` 및 `createManyQuietly` 메서드는 이벤트를 전달하지 않고 모델을 생성하는 데 사용할 수 있습니다.

    $user = User::find(1);

    $user->posts()->createQuietly([
        'title' => 'Post title.',
    ]);
    
    $user->posts()->createManyQuietly([
        ['title' => 'First post.'],
        ['title' => 'Second post.'],
    ]);

You may also use the `findOrNew`, `firstOrNew`, `firstOrCreate`, and `updateOrCreate` methods to [create and update models on relationships](/docs/{{version}}/eloquent#upserts).

`findOrNew`, `firstOrNew`, `firstOrCreate`, `updateOrCreate` 메서드를 [연관관계에 대한 모델 생성 및 업데이트](/docs/{{version}}/eloquent#upserts)에 사용할 수도 있습니다 .

> **Note**
> Before using the `create` method, be sure to review the [mass assignment](/docs/{{version}}/eloquent#mass-assignment) documentation.

> **Note**
> `create` 메서드를 사용하기 전에 [대량 할당-mass assignment](/docs/{{version}}/eloquent#mass-assignment) 문서를 반드시 확인하시기 바랍니다.

<a name="updating-belongs-to-relationships"></a>
### Belongs To Relationships
### Belongs To 연관관계

If you would like to assign a child model to a new parent model, you may use the `associate` method. In this example, the `User` model defines a `belongsTo` relationship to the `Account` model. This `associate` method will set the foreign key on the child model:

하위 모델을 상위 모델에 새롭게 연관관계를 추가하고자 할 때에는 `associate` 메서드를 사용할 수 있습니다. 이 예제에서 `User` 모델은 `Account` 모델에 대한 `belongsTo` 연관관계를 가지고 있습니다. 이 `associate` 메서드는 하위 모델에 외래키를 설정합니다.

    use App\Models\Account;

    $account = Account::find(10);

    $user->account()->associate($account);

    $user->save();

To remove a parent model from a child model, you may use the `dissociate` method. This method will set the relationship's foreign key to `null`:

하위 모델에서 상위 모델과의 연관관계를 제거하고자 할 때에는 `dissociate`메서드를 사용하면 됩니다. 이 메서드는 연관관계 외래키를 `null` 로 설정합니다.  

    $user->account()->dissociate();

    $user->save();

<a name="updating-many-to-many-relationships"></a>
### Many To Many Relationships
### 다대다 연관관계

<a name="attaching-detaching"></a>
#### Attaching / Detaching
#### 연결하기 / 분리하기

Eloquent also provides methods to make working with many-to-many relationships more convenient. For example, let's imagine a user can have many roles and a role can have many users. You may use the `attach` method to attach a role to a user by inserting a record in the relationship's intermediate table:

엘로퀀트는 다대다 연관관계를 다루는 편리한 메서드를 추가로 제공합니다. 예를 들어 한 사용자가 여러 역할을 가질 수 있고 한 역할이 여러 사용자를 갖는다고 상상해봅시다.`attach` 메서드를 사용하여 연관관계 중간 테이블의 레코드를 삽입하여 연관관계를 연결할 수 있습니다. 

    use App\Models\User;

    $user = User::find(1);

    $user->roles()->attach($roleId);

When attaching a relationship to a model, you may also pass an array of additional data to be inserted into the intermediate table:

모델에 연관관계를 연결할 때 중간 테이블에 삽입될 추가 데이터의 배열을 전달할 수도 있습니다.

    $user->roles()->attach($roleId, ['expires' => $expires]);

Sometimes it may be necessary to remove a role from a user. To remove a many-to-many relationship record, use the `detach` method. The `detach` method will delete the appropriate record out of the intermediate table; however, both models will remain in the database:

경우에 따라 사용자에게서 역할을 분리하는 것이 필요할 수 있습니다. 다대다 연관관계의 중간 테이블 레코드을 제거하려면 `detach` 메서드를 이용하면 됩니다. `detach` 메서드는 중간 테이블에서 적절한 레코드를 삭제할 것입니다. 하지만 연관관계를 형성했던 두 모델은 데이터베이스에 그대로 남아 있습니다.

    // Detach a single role from the user...
    $user->roles()->detach($roleId);

    // Detach all roles from the user...
    $user->roles()->detach();

For convenience, `attach` and `detach` also accept arrays of IDs as input:

보다 편한 방법으로, `attach`와 `detach` 메서드에 ID의 배열을 전달할 수 있습니다.

    $user = User::find(1);

    $user->roles()->detach([1, 2, 3]);

    $user->roles()->attach([
        1 => ['expires' => $expires],
        2 => ['expires' => $expires],
    ]);

<a name="syncing-associations"></a>
#### Syncing Associations
#### 연결 동기화

You may also use the `sync` method to construct many-to-many associations. The `sync` method accepts an array of IDs to place on the intermediate table. Any IDs that are not in the given array will be removed from the intermediate table. So, after this operation is complete, only the IDs in the given array will exist in the intermediate table:

`sync` 메서드를 사용하여 다대다 연관관계를 생성 할 수도 있습니다. `sync` 메서드는 중간 테이블 구성할 연관 모델의 ID 배열을 인자로 받습니다. 주어진 배열에 포함되어 있지 않는 ID는 중간 테이블에서 제거됩니다. 따라서 이 작업이 수행되면 배열에 포함된 ID들만 중간 테이블에 남아있습니다.

    $user->roles()->sync([1, 2, 3]);

You may also pass additional intermediate table values with the IDs:

중간테이블 레코드에 추가 컬럼이 있다면 ID와 함께 중간 테이블 레코드 값을 추가로 전달할 수 있습니다.

    $user->roles()->sync([1 => ['expires' => true], 2, 3]);

If you would like to insert the same intermediate table values with each of the synced model IDs, you may use the `syncWithPivotValues` method:

동기화하려는 모델 ID가 있고 모두 동일한 중간 테이블 값을 가지게 하려면 `syncWithPivotValues` 메서드를 사용할 수 있습니다.

    $user->roles()->syncWithPivotValues([1, 2, 3], ['active' => true]);

If you do not want to detach existing IDs that are missing from the given array, you may use the `syncWithoutDetaching` method:

동기화를 수행할 때 주어진 배열에는 포함되어 있지 않지만, 기존에 존재하는 ID 값들을 제거하지는 않고 싶다면 `syncWithoutDetaching` 메서드를 사용할 수 있습니다. 

    $user->roles()->syncWithoutDetaching([1, 2, 3]);

<a name="toggling-associations"></a>
#### Toggling Associations
#### 연결 켜고 끄기(토글)

The many-to-many relationship also provides a `toggle` method which "toggles" the attachment status of the given related model IDs. If the given ID is currently attached, it will be detached. Likewise, if it is currently detached, it will be attached:

다대다 연관관계는 주어진 모델 ID들의 연결 상태를 "전환(토글)" 할 수 있는 `toggle` 메서드를 제공합니다. 주어진 ID가 현재 연결이 있으면 해제됩니다. 마찬가지로 현재 해제되어 있다면 연결될 것입니다.

    $user->roles()->toggle([1, 2, 3]);

You may also pass additional intermediate table values with the IDs:

추가적인 중간 테이블 값을 ID와 함께 전달할 수도 있습니다.

    $user->roles()->toggle([
        1 => ['expires' => true],
        2 => ['expires' => true],
    ]);

<a name="updating-a-record-on-the-intermediate-table"></a>
#### Updating A Record On The Intermediate Table
#### 중간 테이블의 레코드 수정하기

If you need to update an existing row in your relationship's intermediate table, you may use the `updateExistingPivot` method. This method accepts the intermediate record foreign key and an array of attributes to update:

연관관계의 중간 테이블에 있는 레코드를 수정해야하는 경우, `updateExistingPivot` 메서드를 사용할 수 있습니다. 이 메서드는 업데이트할 중간 테이블 레코드의 외래키와 변경할 속성의 배열을 인자로 전달받습니다.

    $user = User::find(1);

    $user->roles()->updateExistingPivot($roleId, [
        'active' => false,
    ]);

<a name="touching-parent-timestamps"></a>
## Touching Parent Timestamps
## 상위 모델의 타임스탬프 값 갱신하기

When a model defines a `belongsTo` or `belongsToMany` relationship to another model, such as a `Comment` which belongs to a `Post`, it is sometimes helpful to update the parent's timestamp when the child model is updated.

`Post`에 소속되는 `Comment`와 같이 한 모델이 다른모델에 `belongsTo`이나 `belongsToMany`와 같은 일대일 일대다의 하위 연관관계를 가지고 있을 때, 하위 모델이 업데이트 되었을 때 상위 모델의 타임스탬프 값을 갱신할 수 있습니다.  

For example, when a `Comment` model is updated, you may want to automatically "touch" the `updated_at` timestamp of the owning `Post` so that it is set to the current date and time. To accomplish this, you may add a `touches` property to your child model containing the names of the relationships that should have their `updated_at` timestamps updated when the child model is updated:

예를 들어 `Comment` 모델이 업데이트되었을 때, 이 모델을 소유하는 `Post`의 `updated_at` 타임스탬프의 값을 자동으로 현재의 시간값으로 "갱신"하고자 할 수 있습니다. 이렇게 하기 위해서는 하위 모델의 `touches` 속성에 연관관계의 이름을 추가하면 됩니다. 이 연관관계 모델은 `updated_at` 타임스탬프를 가지고 있어야 합니다.

    <?php

    namespace App\Models;

    use Illuminate\Database\Eloquent\Model;
    use Illuminate\Database\Eloquent\Relations\BelongsTo;

    class Comment extends Model
    {
        /**
         * All of the relationships to be touched.
         *
         * @var array
         */
        protected $touches = ['post'];

        /**
         * Get the post that the comment belongs to.
         */
        public function post(): BelongsTo
        {
            return $this->belongsTo(Post::class);
        }
    }

> **Warning**
> Parent model timestamps will only be updated if the child model is updated using Eloquent's `save` method.

> **Warning**
> 상위 모델의 타임스탬프값은 하위 모델이 엘로퀀트의 `save` 메서드를 사용해서 업데이트 될 때만 갱신됩니다. 