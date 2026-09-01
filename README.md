# aura-farm-legal

La política de privacidad de **Aura Farm (Aura Farming Simulator)**, más el
`app-ads.txt` de AdMob. Sitio estático de un solo archivo, desplegado en
Vercel.

## Qué hay acá

- **`index.html`** — la política, bilingüe (español / inglés) en una sola
  página. Es la URL que se pega en Google Play (Data Safety) y en el
  mensaje de privacidad de AdMob.
- **`app-ads.txt`** — declara que el publisher `pub-6358243501495774` está
  autorizado a vender inventario de esta app. **Tiene que servirse desde la
  raíz del dominio**, y ese mismo dominio es el que hay que declarar como
  sitio web del desarrollador en la ficha de Play. Sin eso, los rastreadores
  de Google no lo encuentran y la protección no aplica.
- **`vercel.json`** — sólo fuerza el `Content-Type` de `app-ads.txt`. Los
  rastreadores esperan texto plano; servido como `application/octet-stream`
  el archivo se ignora en silencio.

## Desplegar

```bash
vercel --prod
```

O conectando el repo desde el panel de Vercel: es un sitio estático sin
build, así que no hay nada que configurar.

## Después de desplegar

1. **AdMob** → Privacidad y mensajes → GDPR: crear el mensaje y pegar la URL
   de la política. Sin ese mensaje, el formulario de consentimiento de la
   app no tiene qué mostrar en Europa.
2. **AdMob** → Apps → Aura Farm → app-ads.txt: verificar. Puede tardar
   hasta 24h en aparecer como verificado.
3. **Google Play** → Data Safety: declarar lo que dice la sección 3 de la
   política — identificadores del dispositivo recolectados por AdMob para
   publicidad. **La declaración tiene que coincidir con la política**; si
   difieren, Play rechaza la publicación.

## Ojo con esto

El `app-ads.txt` lleva el mismo publisher ID que `ledcoteca-legal`, y es
correcto: es una cuenta de AdMob por desarrollador, no por app. Lo que
cambia entre apps son los ad unit IDs, que viven en el código.
