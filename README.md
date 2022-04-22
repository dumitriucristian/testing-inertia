##Step one - install laravel
[Laravel instalation] https://laravel.com/docs/9.x/installation
```
curl -s https://laravel.build/example-app | bash
cd example-app
 ./vendor/bin/sail up
```

##Create Sail  alias
Go into WSL in the project folder and run 
```
alias sail='[ -f sail ] && bash sail || bash vendor/bin/sail'
```
##Start Sail
```angular2html
sail up -d
```


##Step two - install inertia
Go to [inertia website] https://inertiajs.com/ and install server side adapter
```composer require inertiajs/inertia-laravel```      
replace laravel default page welcome.blade.php with app.blade.php   
set inertia middleware   
set client side adapter
install vue
```npm install vue@next```

install single file components
```
npm install -D @vue/compiler-sfc
```
initialize app copy this code into app.js  
```
import { createApp, h } from 'vue'
import { createInertiaApp } from '@inertiajs/inertia-vue3'

createInertiaApp({
    resolve: name => require(`./Pages/${name}`),
    setup({ el, App, props, plugin }) {
        createApp({ render: () => h(App, props) })
            .use(plugin)
            .mount(el)
    },
})
```
add vue support and versioning copy this code into webpack.mix.js
```
mix.js('resources/js/app.js', 'public/js')
    .vue(3)
    .postCss('resources/css/app.css', 'public/css', [
        //
    ])
    .version();
```
install all with
```
npm install
```
use twice npx mix to compile code
```npx mix```


##Configure Sail hot reload with browser sink
[Sail hot reload]  https://blog.devgenius.io/quick-tip-laravel-mix-hot-reloading-in-sail-with-browsersync-555b6c97bca3
start sail
```angular2html
sail up -d
```

Publish sail
```
sail artisan sail:publish
```
modify webpack
```angular2html
mix.browserSync({
    proxy: 'localhost',
    open: false,
});

```

run
```
sail npm run watch-poll
```
