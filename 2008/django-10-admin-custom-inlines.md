---
title: 'Django 1.0 admin custom inlines'
date: 2008-08-12T03:55:00.000-07:00
oldUrl: "http://ciantic.blogspot.com/2008/08/django-10-admin-custom-inlines.html"
tags : [django-admin, django]
---

```python
  
...  
  
class ChangeSetForm(forms.ModelForm):  
  dosomething = forms.BooleanField(label="Do something")  
  class Meta:  
      model = ChangeSet  
      exclude = ('modified',) # Note: This doesn't work!  
      fields = ('old_title',) # Note: This doesn't work!  
      
ChangeSetInlineFormSet = inlineformset_factory(  
  Article, ChangeSet,  
  form = ChangeSetForm  
)  
  
class InlineChangeSet(admin.TabularInline):  
  model = ChangeSet  
  form = ChangeSetForm  
  extra = 0  
  raw_id_fields = ('editor',)  
  fields = ('old_title', ) # This works.  
  
...  

```

## Completely custom inline (without delete checkbox etc)

  
coming...