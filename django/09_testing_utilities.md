# Testing & Utilities in Django

## 1. Django TestCase
Built on top of `unittest`. Handles DB transaction rollback after each test.

```python
from django.test import TestCase
from .models import Product

class ProductModelTest(TestCase):
    def setUp(self):
        self.product = Product.objects.create(name="Test", price=10)

    def test_product_creation(self):
        self.assertEqual(self.product.name, "Test")
```

## 2. Pytest-Django (Recommended)
More concise, powerful fixtures.

`pip install pytest-django`

**pytest.ini**:
```ini
[pytest]
DJANGO_SETTINGS_MODULE = myproject.settings
python_files = tests.py test_*.py *_tests.py
```

**Test with Pytest**:
```python
import pytest
from .models import Product

@pytest.mark.django_db
def test_create_product():
    product = Product.objects.create(name="Pytest", price=20)
    assert product.pk is not None
    assert Product.objects.count() == 1
```

## 3. Factory Boy
Replace fixtures with factories for creating test data.

```python
import factory
from .models import User

class UserFactory(factory.django.DjangoModelFactory):
    class Meta:
        model = User
    
    username = factory.Sequence(lambda n: f'user{n}')
    email = factory.Faker('email')

# Usage in test
def test_user_factory(db):
    user = UserFactory()
    assert "@" in user.email
```
