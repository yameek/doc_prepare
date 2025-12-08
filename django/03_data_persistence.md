# Data Persistence in Django (ORM)

Django's ORM is its strongest feature, providing a high-level abstraction for SQL database interactions.

## 1. Models
Models are the single source of truth for your data.

```python
from django.db import models

class Category(models.Model):
    name = models.CharField(max_length=100)

    class Meta:
        db_table = "categories" # Explicit table name
        ordering = ["name"]

class Product(models.Model):
    category = models.ForeignKey(Category, on_delete=models.CASCADE, related_name='products')
    name = models.CharField(max_length=200)
    price = models.DecimalField(max_digits=10, decimal_places=2)
    stock = models.IntegerField(default=0)
    is_active = models.BooleanField(default=True)
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    # Custom manager for cleaner queries
    class ActiveManager(models.Manager):
        def get_queryset(self):
            return super().get_queryset().filter(is_active=True)

    objects = models.Manager() # Default manager
    active = ActiveManager()   # Custom manager

    def __str__(self):
        return self.name
```

## 2. One-to-One, Many-to-Many
*   **OneToOneField**: e.g., User Profile.
*   **ManyToManyField**: e.g., Tags on a Post.

```python
class Post(models.Model):
    # ... fields
    tags = models.ManyToManyField("Tag", related_name="posts")
```

## 3. QuerySets (Fetching Data)
Lazy evaluation ensures efficiency.

```python
# Filtering
active_products = Product.active.all()
expensive_stuff = Product.objects.filter(price__gt=1000)

# Chaining
results = Product.objects.filter(category__name="Electronics").exclude(stock=0).order_by("-price")

# Optimization (N+1 Problem)
# select_related = JOIN (Foreign Keys)
# prefetch_related = separate lookup (Many-to-Many / Reverse FK)
params = Product.objects.select_related('category').prefetch_related('tags').all()
```

## 4. Migrations
*   `python manage.py makemigrations`: Generate migration files based on model changes.
*   `python manage.py migrate`: Apply migrations to the DB.
