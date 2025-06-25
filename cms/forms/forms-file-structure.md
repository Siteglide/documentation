# Forms File Structure

```bash
└───marketplace_builder
    ├───custom_model_types
    │   └───forms
    │           form_3.yml
    │
    ├───form_configurations
    │   └───forms
    │           form_3.liquid
    │
    ├───notifications
    │   └───email_notifications
    │       └───forms
    │           └───form_3
    │               └───fic
    │                       0.liquid
    │                       1.liquid
    │
    └───views
        └───partials
            ├───layouts
            │   ├───forms
            │   │   └───form_3
            │   │       default.liquid
            │   │
            │   └───form_confirmation
            │           default.liquid
            │
            └───tables
                └───forms
                        3.liquid
```

* Form Layouts can be modified in the views/layouts/partials/form folder. A reserved file named default.liquid will be created as shown, this will be edited automatically by the system, so if you want to make any modifications, you should always:
  * a) Make a copy and give it a new custom name
  * b) In the 'include' tag, change the layout parameter to point to the new file name
* The notifications folder stores any Liquid files which are used to render automation email notifications or API calls. `fic` refers to `form created.` Files are given an ID starting with 0 and ascending. This must match the ID of the automation in `marketplace_builder/views/partials/tables`
* Ignore the folders `custom_model_types`, `form_configurations` and `views/partials/tables` unless you are creating forms using CLI. It is recommended to create and edit forms using the Siteglide Admin UI as it prevents duplicate work needed to update the several files involved. There may be situations where you would want to edit in CLI, in which case it's recommended to edit the file in the tables folder and then after syncing to save in the Siteglide Admin to apply that change everywhere.
