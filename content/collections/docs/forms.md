---
title: Forms
template: page
id: fdb45b84-3568-437d-84f7-e3c93b6da3e6
blueprint: page
stage: 1
intro: Forms are a natural part of the internet experience and a core component of most websites. From a basic "Contact Me" form to a multi-page job application, Statamic can help manage your forms, submissions, and thereby make your life a little bit easier.
---
## Overview

Statamic forms collect submissions, provide reports and metrics on them on aggregate, and display user submitted data on the [frontend](/frontend). The end-to-end solution includes tags, settings, and a dedicated area of the Control Panel.

## Your First Form

Let's pretend you're are a famous celebrity with a large following of dedicated fans. If this is true, why are you building your own website? Who's going to sail your yacht?

Okay, let's just pretend you're a famous celebrity's _web developer_. You've been tasked with collecting electronic fan mail (we'll call it EF-Mail). You want to collect the following bits of info from <del>crazed</del> enthusiastic fans:

- name
- age
- level of adoration (appreciation, fixation, or obsession)
- message

### Create the form

First, head to `/cp/forms` in the Tools area of the Control Panel and click the **Create Form** button. Alternately you can create a `.yaml` file in `site/settings/formsets` which will contain all the form fields and settings.

Each form should contain a title and a reference to a [blueprint](blueprints). Optionally it may also have metrics and email configuration.

```yaml
title: Super Fans
blueprint: super_fans
```

### The Blueprint

The [blueprint](blueprints) is where you define your form's `fields` and validation rules to be used on form submission.

```yaml
fields:
  -
    handle: name
    field:
      display: Name
      type: text
      validate: required
  -
    handle: age
    field:
      display: Age
      type: text
      validate: required|integer
  -
    handle: adoration
    field:
      display: Level of Adoration
      type: text
      validate: required
  -
    handle: message
    field:
      display: Message
      type: textarea
      validate: required
```

### The Template

Several [tags](tags/form) are provided to help you manage your form. You can explore these at your leisure, but for now here's a look at a basic form template.

This example dynamically renders each input's HTML. You could alternatively write the HTML yourself, perform conditions on the field's `type`, or even [customize the automatic HTML](/tags/form-create#dynamic-rendering).

```
{{ form:super_fans }}

    // First let's check if this is after a submission, and if so, was it successful.
    // If it was, just show the success message. After all, we don't want them submitting again once they've gotten in touch!
    {{ if success }}
        <div class="bg-green-300 text-white p-2">
            {{ success }}
        </div>
    {{ else }}
        // If we weren't successful, show any errors. If a fresh page load, there's no errors, so do nothing.
        {{ if errors }}
            <div class="bg-red-300 text-white p-2">
                {{ errors }}
                    {{ value }}<br>
                {{ /errors }}
            </div>
        {{ /if }}

        // Loop through and render the form inputs
        {{ fields }}
            <div class="p-2">
                <label>{{ display }}</label>
                <div class="p-1">{{ field }}</div>
                {{ if error }}
                    <p class="text-gray-500">{{ error }}</p>
                {{ /if }}
            </div>
        {{ /fields }}

        // This is just a submit button.
        <button type="submit">Submit</button>
    {{ /if }}

{{ /form:super_fans }}
```

## Viewing Submissions

In the Forms area of the control panel you can explore the collected responses, configure dashboards with reporting metrics, and export the data to CSV or JSON formats.

<figure>
  <img src="/img/cp-forms.png" alt="List of form submissions in the control panel">
  <figcaption>Forms. Submissions. Features.</figcaption>
</figure>

## Displaying submission data

You can display any or all of the submissions of your forms on the front-end of your site using the [form submissions][submissions] Tag.

```
<h2>My fans have said some things you can't forget...<h2>
{{ form:submissions in="superfans" limit="15" }}
  {{ message | markdown }}
{{ /form:submissions }}
```

## Exporting your data

Exporting your data is just a click of the **Export** button away. You have the choice between CSV and JSON. Choose wisely, or choose both, it doesn't matter to us.

## Emails

Allowing your fans to send their comments is all well and good, but at this point you will only know about it when you head back into the Control Panel to view the submissions. Wouldn't it be better to get notified? Let's hook that up next.

You can add any number of emails to your formset.

```yaml
email:
  -
    to: hello@celebrity.com
    from: website@celebrity.com
    subject: You've got fan mail!
    html: fan-mail
    text: fan-mail-text
  -
    to: agent@celebrity.com
    subject: Someone still likes your client
    automagic: true
```

Here we'll send two emails for every submission of this form. One will go to the celebrity, and one to the agent. The first one uses Statamic templates while the other gets an "automagic" email. The automagic email will be a simple text email with a list of all fields and values in the submission.

### Setting the Recipient Dynamically

You can set the recipient to an address submitted in the form by using the variable in your config block. Assuming you have a form input with `name="email"`:

```yaml
email:
  -
    to: "{{ email }}"
    # other settings here
```

### Setting the "Reply To" Dynamically

You can set the "reply to" to an address submitted in the form by using the variable in your config block. Assuming you have a form input with `name="email"`:

```yaml
email:
  -
    reply_to: "{{ email }}"
    # other settings here
```

### Setting the "Subject" Dynamically

You can set the set the email "subject" to a value in your form by using the variable in your config block. Assuming you have a form input with `name="subject"`:

```yaml
email:
  -
    subject: '{{ subject ?? "Email Form Submission" }}'
    # other settings here
```

[Learn how to create your emails](/knowledge-base/emails)

## File Uploads

Sometimes your fans want to show you things they've created, like scissor-cut love letters and innocent selfies with cats. No problem! File input types to the rescue. Inform Statamic you intend to collect files, specify where you'd like the uploads to go, and whether you'd like them to simply be placed in a directory somewhere, or become reusable Assets.

First up, add `files="true"` to  your form tag. (This will add `enctype="multipart/form-data"` to the generated `<form>` tag. That's always so difficult to remember.)

```
{{ form:create formset="contact" files="true" }}
...
{{ /form:create }}
```

Then the fields:

```
<input type="file" name="simple" />
<input type="file" name="fancy" />
```

```yaml
fields:
  simple:
    type: file
    destination: uploads/
  fancy:
    type: asset
    container: uploads
    folder: fan-art
```

**Simple Uploads**: Set `type: file` and a `destination` (path from webroot). That's it.

**Asset Uploads**: Set `type: asset`, specify the asset `container` via handle or ID, and which folder inside said container.

### Multiple files

You have two methods available to you:

First, You can create separate fields for each upload. This is useful if each has a separate purpose, like Resume, Cover Letter, and Headshot. You'll need to explicitly create each and every one in your formset.

Or, you can enable multiple files on one field, by setting type with the plural form of the type option, `files` or `assets`, and indicating an array in your input by adding a set of square brackets to the `name` attribute.

```
<input type="file" name="many[]" multiple />
```

```yaml
fields:
  many:
    type: files
    destination: uploads/
```

> If you use the square bracket `name` syntax, but use the singular `type` in your formset, only the first selected file will be uploaded. Don't forget to set both.

## Honeypot

Simple and effective spam prevention.

The honeypot technique is simple. Add a field to your forms, that when filled in will cause the submission to fail.
Hide this field a method of your choosing (ie. CSS), so your users won't see it but spam bots will just think it’s another field.

For example:

```
{{ form:create }}
    ...
    <input type="text" name="honeypot" class="honeypot" />
{{ /form:create }}
```

``` .language-css
.honeypot { display: none; }
```

If you're worried about smarter spam bots realizing that the honeypot field is named `honeypot`, you may customize the
name of the field by adding `honeypot: something` to your formset.

> We say the submission will "fail", but that's not **exactly** true. On the front end it will appear that the form was submitted successfully. However, nothing will get saved and no emails will be sent. This is the key to tricking bots into believing everything went smoothly.

## Using AJAX

To submit the form with AJAX, be sure to pass all the form inputs in with the submission, as Statamic sets `_token` and `_params`, both of which are required.

You'll also need to set your ajax library's `X-Requested-With` header to `XMLHttpRequest'.

### Axios Example

``` javascript
window.axios.defaults.headers.common['X-Requested-With'] = 'XMLHttpRequest';
form = document.getElementById('form');

// On submit...
axios.post(form.action, new FormData(form))
  .then(response => {
      console.log(response.data)
  });
```

[tags]: /tags/form
[submissions]: /tags/form-submissions

