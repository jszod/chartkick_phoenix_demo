# ChartkickPhoenixDemo

To start your Phoenix server:

  * Install dependencies with `mix deps.get`
  * Install Node.js dependencies with `npm install` inside the `assets` directory
  * Start Phoenix endpoint with `mix phx.server`

Now you can visit [`localhost:4000`](http://localhost:4000) from your browser.

Ready to run in production? Please [check our deployment guides](https://hexdocs.pm/phoenix/deployment.html).

## Learn more

  * Official website: https://www.phoenixframework.org/
  * Guides: https://hexdocs.pm/phoenix/overview.html
  * Docs: https://hexdocs.pm/phoenix
  * Forum: https://elixirforum.com/c/phoenix-forum
  * Source: https://github.com/phoenixframework/phoenix

# Installation
## Add Chartkick-ex library

Add chartkick lib to `mix.exs`
```
{:chartkick, "~>0.4.0"}
```

Add uuid to extra applications in `mix.exs`
```
def application do
    [
      ...,
      extra_applications: [..., :uuid]
    ]
```

## Add chartkick.js to application

 **Install chartkick.js and highcharts.js (chart engine) with npm**

 ```
 $ cd assets
 $ npm install chartkick chart.js --save
 $ npm install highcharts.js --save
 ```

 **Create a file chartkick_init.js**

 In `assets/js` create a new file, I named it `chartkick_init.js`. The file can be named anything you want. This file will import the javascript that the chartkick-ex wrapper lib uses.

 The contents of the file simply import the chartkick.js library
 ```
 import 'chartkick'
 import 'highcharts'
 ```
**Update `webpack.config.js`**

Make a new entry point for `chartkick_init.js` so we can load the js only on the pages that it's needed

Edit `assets/webpack.config.js` and add the new `chartkick_init` entry as shown in the `entry` section. Make sure to add the comma at the end of the `app` entry line.
```
entry: {
      'app': glob.sync('./vendor/**/*.js').concat(['./js/app.js']),
      'chartkick_init': glob.sync('./vendor/**/*.js').concat(['./js/chartkick_init.js'])
    },
```

## Update view and templates
    
Add `/lib/chartkick_phoenix_demo_web/views/page_view.ex' contents as shown in the sourece files

Add '/lib/chartkick_phoenix_demo_web/templates/page/index.html.eex` contents as shown in the source files

**Add script tag in `index.html.eex`**

This page needs to load the charkick js libs. Add the following line to import the `chartkick_init.js` file.
```
<script src='<%= Routes.static_path(@conn, "/js/chartkick_init.js") %>' type="text/javascript"></script>
```




