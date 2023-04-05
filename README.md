# Make-factory-for-nested-category

create factory acording this column

```
public function up()
    {
        Schema::create('sub_categories', function (Blueprint $table) {
            $table->id();
            $table->unsignedBigInteger('category_id');
            $table->string('sub_category_name');
            $table->string('sub_category_slug');
            $table->foreign('category_id')->references('id')->on('categories')->onUpdate('cascade')->onDelete('cascade');
            $table->timestamps();
            $table->softDeletes();
        });
    }
```


To create a factory for the given table structure, follow these steps:

1. Define a new factory class that extends the `Illuminate\Database\Eloquent\Factories\Factory` class.
2. In the factory's `definition()` method, return an array with keys corresponding to the columns in the table and values representing their default or generated values.

Here's an example factory implementation for the given table structure:

```
<?php

namespace Database\Factories;

use App\Models\SubCategory;
use Illuminate\Database\Eloquent\Factories\Factory;

class SubCategoryFactory extends Factory
{

    protected $model = SubCategory::class;

    public function definition()
    {
        return [
            'category_id' => function () {
                // retrieve a random category id from the categories table
                return \App\Models\Category::inRandomOrder()->first()->id;
            },
            'sub_category_name' => $this->faker->word,
            'sub_category_slug' => $this->faker->slug,
            'created_at' => now(),
            'updated_at' => now(),
            'deleted_at' => null
        ];
    }
}
```

Make sure to replace `App\Models\SubCategory` with the correct namespace of your subcategory model. You can generate this factory by running the following command:

```
php artisan make:factory SubCategoryFactory --model=SubCategory
```

This should create a factory file named `SubCategoryFactory.php` in your `database/factories` directory.

Once you have created the factory, you can use it to generate fake data for your subcategories table. Here's an example usage:

```
$subcategories = SubCategory::factory()->count(10)->create();
```

This will create 10 fake subcategories using the `SubCategoryFactory` and insert them into your database.
