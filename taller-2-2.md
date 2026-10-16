# Taller 2 – Segundo corte: Investigación sobre React

**Estudiante:** José Vega  
**Asignatura:** Desarrollo Frontend  
**Modalidad:** Individual  
**Tema:** React: fundamentos, utilidad e importancia en la industria

---

## Introducción

El desarrollo web actual necesita interfaces que respondan a las acciones de los usuarios y que puedan mantenerse sin que el código se vuelva difícil de modificar. React es una herramienta que ayuda a organizar ese trabajo mediante componentes reutilizables y una forma declarativa de describir lo que debe mostrarse en pantalla. En este trabajo se explican sus conceptos principales, el problema que busca resolver y algunos ejemplos de su uso en empresas.

## Punto 1. ¿Qué es React?

React es una biblioteca de JavaScript utilizada para construir interfaces de usuario, es decir, la parte de una aplicación con la que las personas interactúan. Con React se pueden crear elementos como botones, formularios, menús, tarjetas y páginas completas, organizándolos en componentes que pueden reutilizarse.

React fue creado originalmente por **Jordan Walke**, ingeniero de Facebook —actualmente Meta—, y se publicó como proyecto de código abierto en **mayo de 2013** [1][2].

### ¿Es una librería o un framework?

React se considera principalmente una **librería**. Una librería ofrece funciones concretas que el programador incorpora cuando las necesita. Un framework, por lo general, establece una estructura más amplia y define más decisiones sobre cómo organizar una aplicación.

React se concentra en construir interfaces. Para otras necesidades, como la navegación entre páginas, la obtención de datos o la configuración del proyecto, se pueden añadir herramientas externas. También existen frameworks construidos alrededor de React, como Next.js. Por eso, React por sí solo no obliga a utilizar una única estructura para toda la aplicación.

### ¿Qué significa que sea declarativo?

Que React sea declarativo significa que el programador describe **cómo debe verse la interfaz según los datos actuales**, en lugar de escribir manualmente cada paso para cambiar los elementos de la página. Por ejemplo, se puede indicar que un mensaje aparezca cuando una variable sea verdadera; React se encarga de actualizar la interfaz cuando cambian los datos correspondientes [3].

## Punto 2. ¿Qué problema resuelve React?

### La dificultad de manipular el DOM manualmente

El DOM es la representación de una página HTML que el navegador permite consultar y modificar mediante JavaScript. En una página sencilla, cambiar un texto o un botón manualmente no es complicado. Sin embargo, en una aplicación con muchos elementos interactivos, el programador debe recordar qué elementos cambiar y en qué momento hacerlo.

Si los mismos datos se muestran en varias partes de la página, cada actualización debe reflejarse correctamente en todos esos lugares. Cuando el código crece, es más fácil que la interfaz muestre información desactualizada o que una modificación afecte otra parte de la aplicación.

### Enfoque imperativo y declarativo

- **Imperativo:** se indican los pasos concretos para lograr un resultado. Por ejemplo, buscar un elemento por su identificador, cambiar su texto y modificar su estilo.
- **Declarativo:** se describe el resultado que debe mostrarse para un estado determinado. React compara la nueva descripción de la interfaz con la anterior y aplica los cambios necesarios.

La diferencia no es que JavaScript deje de utilizarse: React también funciona con JavaScript. Lo que cambia es la manera de organizar las actualizaciones de la interfaz.

### Estado y sincronización de la interfaz

El **estado** representa información que puede cambiar mientras se utiliza la aplicación, como el número de productos de un carrito o si un menú está abierto. Cuando se actualiza el estado mediante las herramientas de React, el componente vuelve a renderizarse y la interfaz se adapta al nuevo valor.

Esto ayuda a mantener los datos y lo que se ve en pantalla relacionados, sin tener que modificar manualmente cada elemento del DOM.

### Importancia de los componentes reutilizables

Los componentes permiten dividir una interfaz grande en partes pequeñas con una función definida. Por ejemplo, una tienda puede tener un componente para las tarjetas de productos y reutilizarlo para mostrar muchos artículos diferentes. Así, una modificación en el diseño de la tarjeta puede aplicarse de forma consistente, sin duplicar todo el código.

## Punto 3. Principales componentes de React

### 3.1. Componentes

Un componente es una parte de la interfaz que se puede crear, combinar y reutilizar. En React moderno, normalmente se define como una función de JavaScript que devuelve JSX.

**Características principales:**
- Divide una aplicación en partes más fáciles de entender.
- Puede contener su propia lógica y representar una sección de la interfaz.
- Puede recibir información por medio de props.
- Puede utilizar estado cuando necesita recordar información que cambia.

**Ejemplo:**

```jsx
function Saludo() {
  return <h1>Hola, bienvenido</h1>;
}

export default Saludo;
```

La función `Saludo` es un componente. Cuando se utiliza como `<Saludo />` dentro de otro componente, React muestra el encabezado que devuelve. Por convención, el nombre de un componente comienza con mayúscula.

### 3.2. JSX

JSX es una sintaxis que permite escribir una estructura parecida a HTML dentro del código JavaScript. No es HTML puro: las herramientas del proyecto transforman JSX para que pueda ejecutarse como JavaScript.

**Características y reglas básicas:**
- Los elementos deben cerrarse, por ejemplo, `<img />`.
- Si se devuelven varios elementos al mismo nivel, deben estar dentro de un elemento contenedor o un fragmento.
- Se utiliza `className` en lugar de `class` para asignar clases CSS.
- Las expresiones de JavaScript se escriben entre llaves `{}`.
- Los nombres de los componentes personalizados comienzan con mayúscula.

**Ejemplo:**

```jsx
function Producto() {
  const nombre = "Cuaderno";

  return (
    <section>
      <h2>{nombre}</h2>
      <p>Producto disponible</p>
    </section>
  );
}
```

En este ejemplo, la variable `nombre` se inserta en el encabezado usando llaves. El `section` agrupa los elementos que el componente devuelve.

### 3.3. Props

Las props (propiedades) son datos que un componente recibe desde el componente que lo utiliza. Permiten que una misma estructura se muestre con información diferente.

**Características principales:**
- Se pasan al componente como atributos.
- Pueden contener textos, números, arreglos, objetos o funciones.
- El componente que las recibe debe tratarlas como datos de solo lectura; si necesita cambiar información, normalmente solicita ese cambio mediante una función o actualiza su propio estado.

**Ejemplo:**

```jsx
function Saludo({ nombre }) {
  return <p>Hola, {nombre}</p>;
}

function App() {
  return (
    <>
      <Saludo nombre="Laura" />
      <Saludo nombre="Carlos" />
    </>
  );
}
```

El componente `Saludo` se reutiliza dos veces. La prop `nombre` cambia en cada uso, por lo que se muestran saludos distintos sin duplicar la definición del componente.

### 3.4. Estado con `useState`

El estado es información que un componente necesita conservar entre renderizados. El Hook `useState` permite declarar un valor de estado y una función para actualizarlo.

**Características principales:**
- Se utiliza dentro de componentes funcionales.
- Devuelve el valor actual y una función para solicitar su actualización.
- Cuando el estado cambia, React vuelve a renderizar el componente para reflejar el nuevo valor.
- No se debe modificar directamente la variable de estado.

**Ejemplo:**

```jsx
import { useState } from "react";

function Contador() {
  const [cantidad, setCantidad] = useState(0);

  return (
    <div>
      <p>Clicks: {cantidad}</p>
      <button onClick={() => setCantidad(cantidad + 1)}>
        Sumar
      </button>
    </div>
  );
}
```

Al principio, `cantidad` vale `0`. Cada vez que se pulsa el botón, se solicita actualizarla con `setCantidad`. React vuelve a renderizar el componente y el número mostrado cambia. Esto permite que la interfaz responda al uso de la aplicación sin modificar el texto manualmente.

### 3.5. Eventos: `onClick` y `onChange`

Los eventos permiten que la interfaz responda a acciones del usuario, como pulsar un botón o escribir en un campo. En JSX, los controladores se asignan con propiedades como `onClick` y `onChange`.

**Características principales:**
- `onClick` se utiliza para responder a un clic.
- `onChange` permite responder a cambios en campos de entrada.
- El controlador suele ser una función que ejecuta la acción necesaria.
- Si la acción cambia el estado, React actualiza la interfaz a partir de ese nuevo estado.

**Ejemplo:**

```jsx
import { useState } from "react";

function Formulario() {
  const [nombre, setNombre] = useState("");

  return (
    <div>
      <label>
        Escribe tu nombre:
        <input
          value={nombre}
          onChange={(evento) => setNombre(evento.target.value)}
        />
      </label>
      <p>Tu nombre es: {nombre}</p>
    </div>
  );
}
```

El campo de texto muestra el valor guardado en `nombre`. Cuando el usuario escribe, `onChange` obtiene el contenido del campo y actualiza el estado. Como resultado, el mensaje de abajo cambia a medida que se escribe. El ejemplo también muestra cómo un evento y el estado trabajan juntos.

## Punto 4. Importancia de React en la industria

### ¿Por qué lo eligen las empresas?

React permite dividir interfaces complejas en componentes, reutilizar código y actualizar la pantalla cuando cambian los datos. Estas características resultan útiles en aplicaciones con muchas interacciones, como redes sociales, tiendas virtuales y plataformas de contenido. No significa que React sea la mejor opción para absolutamente todos los proyectos, pero puede facilitar el mantenimiento cuando una interfaz crece.

### Ecosistema de desarrollo

React cuenta con herramientas que cubren distintas necesidades. Por ejemplo:

- **Vite:** ayuda a crear y ejecutar proyectos durante el desarrollo, además de preparar los archivos para producción.
- **Next.js:** es un framework basado en React que añade convenciones y herramientas para construir aplicaciones web, incluidas funciones de renderizado en servidor.
- **React Developer Tools:** permite inspeccionar componentes y analizar su estado durante la depuración.
- **React Native:** utiliza conceptos de React para crear interfaces de aplicaciones móviles.

Estas herramientas no son todas parte del núcleo de React; forman parte del ecosistema que los desarrolladores pueden elegir según las necesidades del proyecto.

### Comunidad y mantenimiento

React es un proyecto de código abierto. Su desarrollo está coordinado por un equipo de trabajo y cuenta con contribuciones de desarrolladores de diferentes empresas y comunidades [4]. Meta mantiene una participación importante, pero el proyecto también recibe aportes externos. La documentación, las herramientas y la actividad de la comunidad ayudan a resolver dudas y a mantener actualizado el conocimiento sobre la biblioteca.

### Relevancia para un desarrollador front-end

Aprender React puede ser valioso para un desarrollador front-end porque permite comprender cómo organizar interfaces basadas en componentes, gestionar estado y responder a eventos. Además, conocer React facilita el aprendizaje de herramientas relacionadas que se utilizan para construir aplicaciones web. Su relevancia laboral depende del mercado y de cada vacante, por lo que también es importante dominar HTML, CSS, JavaScript, accesibilidad y fundamentos de la web.

## Punto 5. Grandes empresas que utilizan React

### 5.1. Meta: Facebook e Instagram

Meta utiliza React en productos web. En una publicación de ingeniería de 2020, la empresa explicó cómo reconstruyó partes importantes de Facebook.com utilizando React para construir una experiencia interactiva y declarativa [5]. Además, en un artículo técnico sobre la mensajería de Instagram para escritorio, Meta describió una sección desarrollada con componentes funcionales de React y Hooks [6].

**¿Por qué es relevante?** Facebook e Instagram tienen interfaces con actualizaciones frecuentes, múltiples tipos de contenido y muchas interacciones. El uso de componentes y del estado ayuda a organizar partes de esas interfaces y a mantenerlas actualizadas. Estos ejemplos son relevantes porque documentan el uso de React en productos reales de gran escala.

### 5.2. Airbnb

Airbnb también trabaja con React. En un artículo técnico de su equipo de ingeniería, la empresa explicó que adoptó React Testing Library para el desarrollo de pruebas de sus componentes React y describió una migración de miles de archivos de pruebas desde Enzyme [7].

**¿Por qué es relevante?** El caso muestra que React no solo se utiliza para crear elementos visuales: también influye en las prácticas de pruebas y mantenimiento de aplicaciones grandes. La experiencia publicada por Airbnb sirve como evidencia técnica de su trabajo con componentes React, aunque el artículo se centra específicamente en las pruebas y no pretende describir toda la arquitectura del producto.

## Conclusiones

React ofrece una forma organizada de construir interfaces mediante componentes reutilizables y una descripción declarativa de lo que debe mostrarse. En lugar de cambiar manualmente cada elemento de la página, el desarrollador define cómo depende la interfaz de los datos y utiliza el estado para representar información que cambia durante el uso.

Los componentes, JSX, props, `useState` y los eventos son conceptos relacionados: los componentes estructuran la interfaz, JSX describe su contenido, las props permiten compartir datos, el estado conserva información cambiante y los eventos conectan las acciones del usuario con las actualizaciones. Su ecosistema y su uso documentado por empresas como Meta y Airbnb demuestran su aplicación práctica en proyectos reales. Para aprovecharlo correctamente, es necesario comprender los fundamentos de JavaScript y escribir código que sea claro, mantenible y comprobable.

## Referencias

[1] React, “Acknowledgements”. Disponible en: https://react.dev/community/acknowledgements

[2] React, “React Versions” (historial de versiones y publicación como código abierto en 2013). Disponible en: https://react.dev/versions

[3] React, “Describing the UI”. Disponible en: https://react.dev/learn/describing-the-ui

[4] React, “Meet the Team”. Disponible en: https://react.dev/community/team

[5] Meta Engineering, “Tech stack rebuild for a new Facebook.com”, 8 de mayo de 2020. Disponible en: https://engineering.fb.com/2020/05/08/web/facebook-redesign/

[6] Meta Engineering, “Launching Instagram Messaging on desktop”, 26 de julio de 2022. Disponible en: https://engineering.fb.com/2022/07/26/web/launching-instagram-messaging-on-desktop/

[7] Airbnb Engineering & Data Science, “Accelerating Large-Scale Test Migration with LLMs”. Disponible en: https://airbnb.tech/infrastructure/accelerating-large-scale-test-migration-with-llms/

---

**Nota de entrega:** guarda este archivo como `taller-2.md`, súbelo a un repositorio de GitHub y verifica que el formato y los bloques de código se visualicen correctamente. La guía solicita entregar el enlace del repositorio, no solamente el archivo.
