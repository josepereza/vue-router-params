# vue-router-params
Ejemplo de rutas con parametros en  vuejs


https://github.com/vuejs/vue-router/tree/dev/examples


# Named Routes

Sometimes it is more convenient to identify a route with a name, especially when linking to a route or performing navigations. You can give a route a name in the routes options while creating the Router instance:
```
const router = new VueRouter({
  routes: [
    {
      path: '/user/:userId',
      name: 'user',
      component: User
    }
  ]
})

```

To link to a named route, you can pass an object to the router-link component's to prop:
```

<router-link :to="{ name: 'user', params: { userId: 123 }}">User</router-link>
```
This is the exact same object used programatically with router.push():
```
router.push({ name: 'user', params: { userId: 123 }})
```
In both cases, the router will navigate to the path /user/123.

* En la carpeta /src  hay un ejemplo de rutas, menus,barra de direccionamiento,redireccionamientos etc.
  Esta carpeta se ha creado automaticamente al crear el proyecto vuejs con: 
  ```
  #vue create client3
  ```
  Despues se elige la opcion manual y despues la opcion Router. 
