Data Tables (In Django this is set up with the models)

Example:

class Convoy(models.Model):
text = models.CharField(max_length=30)
is_active = models.BooleanField(default=True)
origin = models.CharField(max_length=255)
destination = models.CharField(max_length=255)
user = models.ForeignKey(settings.AUTH_USER_MODEL,
on_delete=models.CASCADE, blank=True, null=True)

    def __str__(self):
        return self.text

This model creates a table with attributes for text,is_active, origin, destination, and user.

Types of keys:

Primary Key: (ex. key given to a convoy)

Natural key: (ex. SSN)

Foreign Key: ( This is the key of some of the attributes on a convoy ex. the category)

class ConvoyCategoryRecord(models.Model):
OPTION_A = 'Safety'
OPTION_B = 'Vehicle Info'
OPTION_C = 'Convoy Checklist'

    CATEGORY_CHOICES = [
        (OPTION_A, 'Safety'),
        (OPTION_B, 'Vehicle Info'),
        (OPTION_C, 'Convoy Checklist'),
    ]

    category = models.CharField(
        max_length=20, choices=CATEGORY_CHOICES, blank=True, null=True)
    user = models.ForeignKey(settings.AUTH_USER_MODEL,
                             on_delete=models.CASCADE, blank=True, null=True)
    convoy = models.ForeignKey(
        Convoy, on_delete=models.CASCADE, blank=True, null=True, related_name="records")
