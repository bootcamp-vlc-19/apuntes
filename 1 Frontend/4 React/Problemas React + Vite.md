# Problemas Vite + React

Algunos problemas que han surgido desarrollando sobre el `vite@create` de React

## Error: `'x' is missing in props validation`

> **Solución:** Añadir a archivo `.eslintrc.cjs` lo siguiente:

```JS
...
"rules": {
  ...
  "react/prop-types": "off"
}
```

## Variables de entono `.env` no funcionan

Variables de entorno accediendo a `process.env` siempre vienen como `undefined`

> **Solución:** En Vite se acceden de otra manera: `import.meta.env`
> Y importante:
> Las variables tienen que empezar con `VITE\_`` para que se puedan leer en el cliente

```

//.env
VITE_API_URL=http://localhost...

//En el código:
import.meta.env.VITE_API_URL
```

Más info: https://vitejs.dev/guide/env-and-mode.html

## Error CORS al hacer una llamada a la API

Eso es debido a que el servidor de desarrollo bloquea las llamadas a otras direcciones

> **Solución:** Añadir esto al archivo `vite.config.js`:

```JS
export default defineConfig({
  ...
  server: {
    proxy: {
      '/api': {
        target: 'http://localhost:4000', //vuestro express
        changeOrigin: true,
        rewrite: (path) => path.replace(/^\/api/, ''),
      },
      cors:"false"
    },
  },
})
```

Luego en el `.env` cambiamos la URL de la API para:

```
VITE_API_URL=http://localhost:5173/api
```

Atención al `/api`, es importante

(Sí, la misma dirección que está nuestro React ejecutandose. El servidor de desarrollo reenviará todos los request a la dirección que toca)

> Probablemente hay otra forma de mejor resolverlo, pero bueno.. estuve un buen rato y esto me ha funcionado : )
