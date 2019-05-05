---
title: Images
# tags: [formatting]
#keywords: popovers, tooltips, user interface text, glossaries, definitions
last_updated: May 1 2019
#summary: "You can add tooltips to any word, such as an acronym or specialized term. Tooltips work well for glossary definitions, because you don't have to keep repeating the definition, nor do you assume the reader already knows the word's meaning."
#sidebar: primary_sidebar
permalink: assets_images.html
folder: assets
---

## Introduction

The SafeTow application has

## Application Images

__These images are part of the SafeTow application and are static. They appear in pre-selected areas to give meaning and context to interactions within the application.__

These images are stored in the Ruby on Rails project folder at the path `/app/assets/images`.

Whenever an image is placed here, it should be optimized in Photoshop to be the exact dimensions of how it will appear in the application. Oversized images that are shrunk down in the UI should be avoided because of file size.

Photographs taken from cameras should always be stored as `.jpg` files and computer generated images should always be stored as `.png` or `.gif`.

The following example code shows how to reference an image stored in the assets folder. The example is in __.haml__ format, and features both alt text to describe the image and an additional css class.

```ruby
= image_tag("placeholder-image.png", alt: "placeholder", :class => "max-100")
```

## User-uploaded Images

__These images are uploaded by users of the SafeTow application. Some examples include profile pictures and images of drivers licenses.__

User uploaded images are managed by the `neo4jrb-paperclip` gem, and uploaded to Amazon's S3 service with the `aws-sdk-s3` gem.

An example class with this set up is the [Document](/classes_document.html).

Notice how the Document class uses a property titled `has_neo4jrb_attached_file :attachment` rather than the typical `property :attachment`. The `:styles` property allows to you set the resizing and crop settings of the image as it is uploaded. In the database, a reference path to the Amazon S3 bucket is stored in the `:attachment` property.

```ruby
has_neo4jrb_attached_file :attachment,
                          :styles => {
                              :thumb => "100x100#",
                              :small  => "200x200#",
                              :medium => "560x560#" ,
                              :original => "1200x1200>" },
                          :convert_options => {
                              :thumb => "-quality 75 -strip" }
validates_attachment_content_type :attachment, :content_type => ["image/jpg", "image/jpeg", "image/png", "image/gif"]
```

When users upload images to the SafeTow application, the image gets stored in an Amazon S3 bucket titled [safetow.network](https://s3.console.aws.amazon.com/s3/buckets/safetow.network/?region=us-east-1). The settings for this are determined in each _environment settings file_. These settings must be set individually for each different development environment, although they can all have uniform values.

For example, in `app/config/development.rb` you will find the following excerpt.

```ruby
Paperclip.options[:command_path] = "/usr/local/bin/"

config.paperclip_defaults = {
    :storage => :s3,
    # :s3_host_name => 'REMOVE_THIS_LINE_IF_UNNECESSARY',
    :s3_credentials => {
        :access_key_id => "AKIAJOFLZ6FIMONIXZ4A",
        :secret_access_key => "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",
        :s3_region => "us-east-1"
    },
    :bucket => 'safetow.network'
}
```
