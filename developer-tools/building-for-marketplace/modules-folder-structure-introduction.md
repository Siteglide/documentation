# File Structure

In general there are two main types of folder structure for Modules, though within that, there will be variation on the types of file available, so check each individual module.

The form directory stores the form layout for Module create/ edit Forms.

## Siteglide Published Modules

Most Siteglide published Modules will have a folder structure a little like this:

```
marketplace_builder/
    └── views/
        └── partials/
            └── layouts/
                └── modules/
                    └── module_3/
                        └── example_layout_name/
                        |   └── list/
                        |   |   |── wrapper.liquid
                        |   |   └── item.liquid
                        |   └── detail/
                        |       |── wrapper.liquid
                        |       └── item.liquid
                        └── form/
                            └── example_layout_name.liquid
```

## Newer Siteglide Published Modules & Marketplace Modules

```
modules/
    └── example_module_id/
        └── private/
        └── public/
            └── views/
                └── partials/
                    └── layouts/
                        └── modules/
                            └── module_3/
                                └── example_layout_name/
                                |   └── list/
                                |   |   |── wrapper.liquid
                                |   |   └── item.liquid
                                |   └── detail/
                                |       |── wrapper.liquid
                                |       └── item.liquid
                                └── form/
                                    └── example_layout_name.liquid
```

{% hint style="info" %}
The private folder will exist, but will not be possible to pull using CLI or view in the Code Editor UI. It is for storing functional code which will be used by the Module behind the scenes.
{% endhint %}

Read more about Module Directory Structure on platformOS: [https://documentation.platformos.com/developer-guide/platformos-workflow/directory-structure#modules](https://documentation.platformos.com/developer-guide/platformos-workflow/directory-structure#modules)
