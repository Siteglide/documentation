# Custom Fields in Pages

You can add custom field data to your Pages under the 'Custom Fields' tab.

There will be two available views - one where you control the structure of the data, and one where you control the values. The tabs show depending on what user permissions you have ('CMS - Pages - Custom Fields - Structure' and 'CMS - Pages - Custom Fields - Values')

Once fields have been added under 'Structure' and the 'Save Structure' button has been clicked, your fields will appear under the 'Values' tab.

You can enter your custom field data, and then click 'Save Changes' in the bottom bar on your screen.

Your field data will then be available in your page code using `{{page.metadata.custom_fields.my_field_name.value}}`, where 'my\_field\_name' is the ID of your field.
