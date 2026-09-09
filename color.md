# CONQUEST Color System

> Fuente de referencia para la identidad visual de CONQUEST. Los tokens definidos aqui deben
> mantenerse alineados entre `olympx-mobile`, `olympx-web` y `olympx-admin`.

## Principios

- Usar `primary` para la accion o elemento visual principal de una pantalla.
- Usar `secondary` para acciones secundarias, navegacion activa y estados destacados.
- Usar la escala `info` para comunicacion, enlaces, informacion y estados informativos.
- Usar la escala `success` para confirmaciones, progreso positivo y objetivos completados.
- Reservar blanco y negro para superficies neutras, iconos y contenido de alto contraste.
- Usar `#000000` como fondo base de la aplicacion; reservar `#0F1B38` para el degradado de marca.
- No introducir colores aislados en componentes si existe un token equivalente.

## Tokens

```json
{
  "colors": {
    "primary": "#222284",
    "secondary": "#2F2DB4",
    "white": "#FFFFFF",
    "black": "#000000",
    "info": "#0D8AC5",
    "infoLight": "#3AB8F2",
    "infoSoft": "#BCE7FB",
    "infoTint": "#E7F6FD",
    "success": "#20A585",
    "successLight": "#4FDEBC",
    "successSoft": "#9CECDA",
    "successTint": "#EAFBF7"
  }
}
```

## Referencia visual

| Token | Hex | Uso recomendado |
| --- | --- | --- |
| `primary` | `#222284` | Marca, CTA principal, seleccion activa |
| `secondary` | `#2F2DB4` | Acciones secundarias y elementos destacados |
| `white` | `#FFFFFF` | Texto sobre fondos oscuros y superficies claras |
| `black` | `#000000` | Texto de maximo contraste y detalles neutros |
| `info` | `#0D8AC5` | Enlaces, informacion y acciones informativas |
| `infoLight` | `#3AB8F2` | Hover, progreso o variacion luminosa de `info` |
| `infoSoft` | `#BCE7FB` | Fondos suaves, bordes y estados informativos ligeros |
| `infoTint` | `#E7F6FD` | Superficies informativas de muy bajo contraste |
| `success` | `#20A585` | Exito, confirmacion y progreso completado |
| `successLight` | `#4FDEBC` | Hover y estados positivos secundarios |
| `successSoft` | `#9CECDA` | Fondos suaves y bordes de exito |
| `successTint` | `#EAFBF7` | Superficies de exito de muy bajo contraste |

El logo de interfaz utiliza `#FFFFFF` y `#00608C` en su degradado interno y tiene fondo transparente
para poder colocarse sobre cualquier superficie. Los iconos nativos usan una variante con fondo negro
(`#000000`) de forma consistente y no deben recibir filtros, tintes ni recoloreado desde los componentes.

## Degradado de marca

El degradado principal combina azul luminoso con azul marino. Se recomienda usarlo en heroes,
headers destacados, tarjetas de progreso o fondos de campanas, no como fondo de toda la interfaz.

```css
background: linear-gradient(
  135deg,
  #75AEF3 0%,
  #75AEF3 40%,
  #0F1B38 60%,
  #0F1B38 100%
);
```

Distribucion de referencia:

- `40%`: `#75AEF3`, azul luminoso.
- `60%`: `#0F1B38`, azul marino.
- Direccion recomendada: `135deg`.

## Tipografia

CONQUEST utiliza dos familias complementarias en mobile y admin:

| Familia | Rol | Aplicacion |
| --- | --- | --- |
| `League Spartan` | Principal | Titulos, cifras destacadas, nombres de secciones y jerarquia visual |
| `Poppins` | Secundaria | Texto corrido, formularios, tablas, etiquetas, botones y ayudas |

### Escala recomendada

- `League Spartan ExtraBold`: display y cifras de alto impacto.
- `League Spartan Bold`: titulos principales y encabezados.
- `League Spartan SemiBold`: subtitulos y encabezados secundarios.
- `Poppins Regular`: texto corrido y contenido de formularios.
- `Poppins Medium`: captions, metadatos y texto auxiliar.
- `Poppins SemiBold`: labels, tabs y acciones secundarias.
- `Poppins Bold`: acciones o datos que necesiten mayor enfasis sin convertirse en titulo.

### Archivos y carga

- Mobile usa archivos estaticos `.ttf` en `olympx-mobile/assets/fonts/` para compatibilidad
  entre iOS y Android.
- Admin usa `LeagueSpartan-VariableFont_wght.ttf` y archivos estaticos de Poppins en
  `olympx-admin/src/assets/fonts/`.
- Los archivos de fuentes tienen licencia OFL; conservar los archivos `OFL.txt` originales.
- No usar `System`, `Arial` u otra familia como estilo principal salvo como fallback del navegador
  o del sistema operativo.

## Reglas de implementacion

- Definir estos valores como tokens del sistema visual, no como valores hexadecimales repetidos.
- Mantener los nombres semanticos aunque cambie un valor hexadecimal en el futuro.
- Verificar contraste WCAG AA para texto, botones y estados antes de publicar una pantalla.
- En fondos `primary`, `secondary` o marino usar texto `white`.
- En fondos `infoTint` o `successTint` usar el color de escala fuerte correspondiente para texto e iconos.
- Los nombres `Light`, `Soft` y `Tint` indican intensidad visual; no representan estados funcionales
  adicionales.
- Aplicar `League Spartan` a la jerarquia de titulos y `Poppins` al contenido operativo.

## Estado

- Definicion: paleta y tipografia base de CONQUEST.
- Alcance actual: mobile y admin.
- Estado: tokens integrados; pendiente validar contraste en todas las pantallas MVP.
