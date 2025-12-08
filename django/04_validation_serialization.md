# Validation & Serialization in Django

Django handles validation via **Forms** (traditional HTML) and **Serializers** (APIs via DRF).

## 1. Django Forms (For HTML Views)
Encapsulate validation logic and HTML generation.

```python
from django import forms
from django.core.exceptions import ValidationError

class ContactForm(forms.Form):
    subject = forms.CharField(max_length=100)
    email = forms.EmailField()
    message = forms.CharField(widget=forms.Textarea)

    def clean_subject(self):
        data = self.cleaned_data['subject']
        if "spam" in data.lower():
            raise ValidationError("Invalid subject line")
        return data
```

## 2. DRF Serializers (For REST APIs)
Convert complex data (Models) to native Python datatypes (JSON) and validate incoming data.

```python
from rest_framework import serializers
from .models import Product

class ProductSerializer(serializers.ModelSerializer):
    # Custom calculated field
    discounted_price = serializers.SerializerMethodField()

    class Meta:
        model = Product
        fields = ['id', 'name', 'price', 'discounted_price', 'category']
        read_only_fields = ['id']

    def get_discounted_price(self, obj):
        return obj.price * 0.9

    # Field-level validation: validate_<field_name>
    def validate_price(self, value):
        if value <= 0:
            raise serializers.ValidationError("Price must be positive.")
        return value

    # Object-level validation
    def validate(self, data):
        if data['name'] == "Test" and data['price'] < 10:
             raise serializers.ValidationError("Test products cannot be cheap.")
        return data
```

## 3. Usage inside Views
```python
# Deserialization & Validation
serializer = ProductSerializer(data=request.data)
if serializer.is_valid():
    serializer.save() # Calls .create() or .update() on the serializer
    return Response(serializer.data, status=201)
else:
    return Response(serializer.errors, status=400)
```
