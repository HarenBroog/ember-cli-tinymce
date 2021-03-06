# Ember-cli-tinymce

This ember-cli addon provides you with a wysiwyg-editor component, based on [TinyMCE](https://www.tinymce.com/)

## Demo

[Demo page](http://marucjmar.github.io/ember-cli-tinymce)

## Installation
To get started simply install the addon:

     ember install ember-cli-tinymce

### Component

```hbs
{{tinymce-editor options=options value=text}}
```

 - *options* attribute is full powered to [tinymce documentation](https://www.tinymce.com/docs/configure/). Changing the options will cause the editor to reload.
 - *value* - the html text generated by editor.

If you need to display the *value*, use the *{{{value}}}* helper for HTML text in the handlebars to prevent escaping.

## Data down actions up

By default the value is updated in the addon. If you want to follow the data-down-actions-up guidlines please define the onValueChanged action.

```hbs
{{tinymce-editor options=options value=text onValueChanged=(action "myOnChangedAction")}}
```

and in your controller

```js
  actions:{
    ...
    myOnChangedAction (value) => {
      // Do something with the value. 
      // At least the text should be updated:
      this.set('text', value)
    }
  }
```

Or, as a shorthand using the `mut` helper:

```hbs
{{tinymce-editor options=options value=text onValueChanged=(action (mut text))}}
```

### Including TinyMCE

You can load TinyMCE from a CDN:

```js
ENV:{
  ...,
  tinyMCE:{
    version: 4 //default 4.4
  }
}
```

Be aware *ver* is a semver reflection of the Tinymce CDN which can introduce issues if a bad release is automatically picked up by your application

Set this to `false` to disable including automatically:

```js
ENV:{
  ...,
  tinyMCE:{
    load: false
  }
}
```

And you can load it in your routes like so:

```js
beforeModel(){
  this._super(...arguments);
  if (typeof tinymce == 'undefined'){
    return Ember.$.getScript('//cdn.tinymce.com/4/tinymce.min.js');
  }
}
```

## My reputation
If you used and love this addon You can help me with my reputation, when you give me a star on github :+1: :star:


## MIT License

This README outlines the details of collaborating on this Ember addon.

For more information on using ember-cli, visit [http://ember-cli.com/](http://ember-cli.com/).
