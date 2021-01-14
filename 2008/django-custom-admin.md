---
title: 'Django 1.0 custom admin two fields shown as one'
date: 2008-08-18T04:44:00.000-07:00
oldUrl: "http://ciantic.blogspot.com/2008/08/django-custom-admin.html"
tags : [django-admin, django]
---

I needed a way to have two model fields to be shown/edited on one form field. And I came up with the following.  
  
(CurrencyField (expense) shows and edits fields `value` and `currency` in the actual model)  
  
```python
from django.contrib import admin  
from budget.models import Expense  
from django import forms  
from django.forms.util import ValidationError  
  
class CurrencyField(forms.CharField):  
   def clean(self, value):  
       amount = 0  
       currency = ''  
       try:  
           amount = float(value.split(" ")[0].strip())  
       except (ValueError, TypeError), te:  
           raise ValidationError('Amount is incorrect!')  
        
       try:  
           currency = value.split(" ")[1].strip().upper()  
           if len(currency) != 3:  
               raise TypeError('cur')  
       except (ValueError, TypeError), te:  
           raise ValidationError('Currency is incorrect! Should be three letter universal sign (e.g. EUR)')  
        
       return (amount, currency)  
  
class ExpenseForm(forms.ModelForm):  
   expense = CurrencyField()  
   def __init__(self, *args, **kwargs):  
       super(ExpenseForm, self).__init__(*args, **kwargs)  
       self.initial['expense'] = "%s %s" % (self.instance.value or '',  
                                            self.instance.currency or '')  
    
   def save(self, commit=True):  
       self.instance.value, self.instance.currency = self.cleaned_data['expense']  
       return super(ExpenseForm, self).save(commit)  
    
   class Meta:  
       model = Expense  
  
# Note added:  
# Expense is like this:  
# class Expense(models.Model):  
#     ...  
#     value = models.FloatField(...)    # This contains the amount of currency, like 120.32  
#     currency = models.CharField(...)  # Currency is e.g. 'USD', 'EUR' identifier of currency  
#     ...  
  
class ExpenseAdmin(admin.ModelAdmin):  
   list_display = ('date', 'time', 'local_currency', 'in_euro', 'description', 'tags')  
   ordering = ('date','time')  
   form = ExpenseForm  
   fields = ('expense', 'date', 'time', 'description', 'tags')  
    
admin.site.register(Expense, ExpenseAdmin)  

```