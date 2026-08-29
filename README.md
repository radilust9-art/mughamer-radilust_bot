# Mughámer — página propia

La página del asistente de Radilust Experience. Es **una sola página**, sin instalación
ni compilación: se sube tal cual y funciona.

```
index.html    ← la página entera (estilos, chat, idiomas y logo, todo dentro)
icono.svg     ← el icono de la pestaña (el mismo de radilustexperience.com)
icono.png     ← el icono para el móvil, cuando alguien la guarda en la pantalla de inicio
vercel.json   ← ajustes de seguridad y caché
```

---

## 1. Subirla a GitHub

1. En GitHub, **New repository**. Nombre: `mughamer-web`. Déjalo **privado** si prefieres.
2. No marques nada más (ni README, ni .gitignore).
3. En la pantalla siguiente, pulsa **uploading an existing file** y arrastra los cuatro
   archivos de esta carpeta.
4. **Commit changes**.

## 2. Publicarla en Vercel

1. Entra en [vercel.com](https://vercel.com) con tu cuenta de GitHub.
2. **Add New → Project** y elige el repositorio `mughamer-web`.
3. Vercel dirá que el framework es *Other*. Está bien: **no toques nada**, no hay nada
   que compilar.
4. **Deploy**.

En menos de un minuto tendrás una dirección tipo `mughamer-web.vercel.app`. Esa ya se
puede compartir.

## 3. Ponerle la dirección propia

Para que sea `mughamer.radilustexperience.com`:

1. En Vercel: **Settings → Domains → Add**, y escribe `mughamer.radilustexperience.com`.
2. Vercel te dará un registro **CNAME** (algo como `cname.vercel-dns.com`).
3. Ese registro hay que añadirlo donde esté contratado el dominio de Radilust. Es un
   cambio pequeño y no afecta a la web actual: solo crea un subdominio nuevo.
4. En cuanto el dominio propague (de minutos a un par de horas), Vercel le pone el
   candado (HTTPS) solo.

La página no lleva ninguna dirección suya escrita dentro, así que cambiar de dominio no
obliga a tocar nada.

---

## Los idiomas

Arriba del todo, debajo del nombre, hay cuatro botones: **Español · Français · English ·
العربية**. Al pulsar uno cambia toda la página — el saludo, los botones, la caja de
escribir y el aviso del pie — **sin gastar nada**, porque no se llama al asistente.

- La primera vez se elige solo, mirando el idioma del navegador del visitante. Si no es
  ninguno de los cuatro, se queda en español.
- La elección se recuerda para la próxima visita.
- En árabe la página entera se da la vuelta (de derecha a izquierda) y usa la tipografía
  árabe de la web de Radilust.
- El menú son cinco botones con icono, colgados justo debajo del saludo. Los iconos son
  del juego **lucide**, el mismo que usa radilustexperience.com, y sustituyen a los
  números que había antes.
- Cada botón **manda la frase entera en el idioma elegido**, no el número. Así Mughámer
  sabe en qué idioma tiene que contestar desde el primer mensaje. Quien prefiera escribir
  "3" a mano también funciona: el asistente sigue entendiendo los números.
- Si el visitante cambia de idioma cuando **ya ha empezado a hablar**, la conversación
  no se borra: solo cambia lo de alrededor.

---

## Lo que se puede cambiar sin saber programar

Todo está junto, al principio del bloque `<script>` de `index.html`, bajo el rótulo
**CONFIGURACION**:

| Qué | Dónde | Para qué |
|---|---|---|
| `CEREBRO` | la dirección del chat en n8n | solo si se cambia de servidor o se rehace el flujo |
| `WHATSAPP` y `TELEFONO` | +34 632 52 63 62 | es lo que se le ofrece al visitante **si el asistente no responde** |
| `PRIVACIDAD` | el enlace legal del pie | si cambia la dirección de la política de privacidad |
| `HORAS_SESION` | 24 | cuántas horas recuerda la conversación de quien vuelve |
| `IDIOMAS` | los cuatro idiomas enteros | saludo, atajos, pie y textos de cada idioma, todos juntos |
| `ICONOS` | los cinco iconos del menú | van por orden: si cambias el orden de los atajos, cambia también el de los iconos |

Dentro de `IDIOMAS`, cada atajo son **dos textos**: `["lo que pone el botón", "lo que se
le manda a Mughámer"]`. El primero es lo que ve el visitante; el segundo es el mensaje
que sale.

> **Ojo con el saludo:** el saludo también existe dentro de n8n, en el nodo *Ventana de
> chat*. El que ve la gente en esta página es el de aquí — el de n8n solo aparece si
> alguien abre la ventana de chat propia de n8n. El de n8n sigue teniendo la lista
> numerada del 1 al 5, y así está bien: ahí no hay botones. Si cambias uno y quieres que
> digan lo mismo, cambia los dos.

---

## Detalles que conviene saber

- **Móvil.** Probada a 360 y 375 px de ancho: los cuatro idiomas caben en una sola fila y
  el pie llega justo al borde inferior. En el móvil, la tecla Intro hace salto de línea y
  se envía con el botón; en el ordenador, Intro envía.
- **Enlaces, correos y teléfonos** que dé el asistente se vuelven pulsables solos.
- **Si el asistente no contesta** (servidor caído, corte de red), el visitante no se queda
  en blanco: se le ofrece el WhatsApp del equipo y el teléfono.
- **El aviso del pie**, en los cuatro idiomas, dice cuatro cosas: que Mughámer es un
  asistente automático, que las gestiones personales las lleva el equipo (con el teléfono
  +34 632 52 63 62, pulsable para llamar), que se guardan los datos que deje el visitante
  para poder atender su solicitud, y el enlace a la política de privacidad de Radilust.
  Es lo que toca, porque el asistente sí recoge esos datos.
- **El teclado del móvil no tapa la caja de escribir.** Cuando el teclado se abre, la página
  se ajusta al alto que de verdad se ve, y vuelve al normal al cerrarlo. Probado dejando
  la pantalla en 420 px de alto: la caja de escribir y el aviso siguen visibles.
- **En el navegador de quien visita** solo se guardan dos cosas: un identificador de
  conversación, para que Mughámer no pierda el hilo si recarga la página, y el idioma
  elegido. Nada más.
- **Nada de lo que escribe el asistente puede colarse como código**: el texto se limpia
  antes de pintarlo.

## Lo que esta página **no** hace

- No lleva analítica ni ningún rastreador.
- No pide cookies, porque no pone ninguna.
- No sube archivos ni audio: solo texto.
