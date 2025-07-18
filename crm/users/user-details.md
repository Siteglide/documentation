# User Details

The user\_details Layout contains the User's name, email and Custom Field Set Data. It can also be used as a container for other CRM Layouts.

## Prerequisites

* This Layout must be outputted inside a Page protected by a Secure Zone

You can use the following links to learn how to set up a Secure Page and the means to access it:

* [Create a Secure Zone](../quickstart-crm.md#2-creating-and-editing-a-secure-zone)
* [Create a Secure Zone Sign Up Form](../quickstart-crm.md#2-adding-a-sign-up-form)
* [Add a Secure Zone to a Page](../quickstart-crm.md#3-securing-pages)

## Introduction

The `user_details` Layout contains a `{{this}}` object with the basics of the User, as well as details that have been added to the CRM record via Custom Field Sets.

As such, it can be useful (though it is optional) to use this Layout as the container for all other CRM Layouts. This allows other Layouts e.g. `user_secure_zones` to also have access to both their specialist data and the more general User data, allowing you to build more complex Layouts.

## Syntax

```liquid
{% include 'user_details', layout: 'default' %}
```

Parameters:

* `layout` - Choose a Layout to use.

## File Structure

You can find the `user_details` Layouts at the following path in Code Editor: `layouts/modules/module_5/user_details/`

Inside this folder, a single Liquid file can be created to act as your Layout. There is no "wrapper" and "item" file needed for this kind of Layout.

## Developing the Layout

### Available Standard Fields

* `{{this.name}}`
* `{{this.first_name}}`
* `{{this.last_name}}`
* `{{this.email}}`
* `{{this.created_at}}` - The date the User first signed up or submitted a Form on the Site
* `{{this.updated_at}}` - The last date the User's CRM data was updated
* `{{this['Company']}}` - An array of Companies this User is connected to
* `{{this['Address']}}` - An array of Addresses stored against this User

### Accessing Custom CRM Fields

Inside a user\_details Layout, you can access custom CRM fields by using:

* `{{this.properties.user_field_1}}` - To get the Field by it's field ID

### Accessing Custom Field Sets

Accessing Custom Field Sets will depend on the Custom Field Set data you have set up on your Site. Each Custom Field Set has a unique ID number assigned to it, and data is organised based on this number.

#### Accessing data from a Custom Field Set by a specific Custom Field Set ID

Custom Field Sets allow you to store custom fields directly against a Module Item. In the case of the CRM, they are used to store fields against a User which can be kept up-to-date. You can learn more about [Custom Field Sets](editing-a-users-crm-record-front-end-with-custom-field-sets.md) here.

In the following example, I'll be accessing data from the Custom Field Set 3 (Profile). You can use this example and replace the ID 3 for the ID of your Custom Field Set.

* `{{this.custom_field_sets.cfs_3.cfs_name}}` - The name of this Custom Field Set
* `{{this.custom_field_sets.cfs_3.properties.cfs_field_3_1}}` - The first field of the Custom Field Set. Replace the ID number at the end to fetch any field.

You may find it more helpful to output your available fields as JSON and use this to write your code.

Outputting `{{this}}` will fetch the data as JSON, e.g.
