---
title: ParameterAttributes
# tags: [formatting]
#keywords: popovers, tooltips, user interface text, glossaries, definitions
last_updated: April 2019
#summary: "You can add tooltips to any word, such as an acronym or specialized term. Tooltips work well for glossary definitions, because you don't have to keep repeating the definition, nor do you assume the reader already knows the word's meaning."
#sidebar: primary_sidebar
permalink: modules_parameter_attributes.html
folder: modules
---

# #TODO REMOVE THIS MODULE

The purpose of this module is to get traditional forms working together nicely with Neo4j.rb. The idea is related to controllers, and the way in which parameters are permitted.

The module is titled **parameter attributes**, because it allows the definition of **parameters** as the **attributes** of a class.

There would be no other way to allow nested forms to work with neo4j.rb without this module. This is because the functionality for permitting the nested parameters in rails is stored by default in ActiveRecord, where we use ActiveNode instead.

## Example usage

Imagine you have a form that you want a user to enter in their phone number and email address, and that will create a ContactInfo object, a Phone object, and an Email object. If you try to pass in parameters like ":phone_number" or ":email_address", then the rails controller will block it because they are not validly part

In each class that this module is included on, you will have to include the following two methods, and fill them in appropriately. I have used the example for the [ContactInfo](/classes_contact_info.html) class.

You will notice that for the *return_model_symbol* class method you are returning the class name with corresponding format, and the *return_parameters_symbol* returns a nested array of anything you would want to pass through a nested form.

```ruby
class ContactInfo

 # ~~~ rest of class is omitted

  def self.return_model_symbol
    model_symbol = :contact_info
    return model_symbol
  end

  def self.return_parameters_symbol
    parameters_symbol = [:addresses => [:description, :nick_name, :street, :city, :state_prov, :postal_code, :country], :phones => [:sort_order, :description, :calling_code, :area_code, :number, :extension], :emails => [:sort_order, :description, :address], :websites => [:sort_order, :description, :url]]
    return parameters_symbol
  end

  # ~~~ rest of class is omitted

end
```

## Modules

| Module | Description |
|-+-|
| ActiveSupport::Concern | Rails 3 introduced a module named ActiveSupport::Concern which has the goal of simplifying the syntax of modules. |

## Methods

## Class Methods
