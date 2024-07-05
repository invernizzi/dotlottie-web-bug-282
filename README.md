
Please ignore this repo - it's a bug reproduction for https://github.com/LottieFiles/dotlottie-web/issues/282

## Create a website that works as expected in dev mode

Create nuxt project.
```
npx nuxi@latest init project
cd project
```

Install dotlottie-web.
```
npm install @lottiefiles/dotlottie-web
```

Download an example dotlottie file ([source](https://dotlottie.io/structure/#interactivity-structure)).
```
 wget 'https://dotlottie.io/sample_files/animation.lottie' -O public/animation.lottie
```

Create `app.vue` to match [its current contents](project/app.vue).


Finally, run `npm run dev` and open the website. 
Two animations will work correctly.
The first one is loaded via `src`, while the other bypasses the bug by loading data through `data`.

![dev images](images/dev.png)

## Reproduce the bug

Build the website for production.
```
npm run build
```

Preview the website as if it was in production.
```
npm run preview

# Or, `node ./server/index.mjs`, which does mostly the same thing.
```

Note that the animation loaded via `src` is not played. The other one is.

![prod images](images/prod.png)
