# 🧠 Preguntas de Entrevista sobre React - Traducción al Español

## 🧩 Core React

## React Básico

### 1. ¿Qué es React?

    React (también conocido como React.js o ReactJS) es una **biblioteca JavaScript de front-end de código abierto** que se utiliza para construir interfaces de usuario componibles, especialmente para aplicaciones de una sola página (SPA). Se encarga de la capa de vista en aplicaciones web y móviles basadas en componentes utilizando un enfoque declarativo.

    React fue creado por [Jordan Walke](https://github.com/jordwalke), un ingeniero de software que trabajaba en Facebook. React se implementó por primera vez en el News Feed de Facebook en 2011 y en Instagram en 2012.

### 2. ¿Cuál es la historia detrás de la evolución de React?

    La historia de ReactJS comenzó en 2010 con la creación de **XHP**. XHP es una extensión de PHP que mejoró la sintaxis del lenguaje de modo que los fragmentos de documentos XML se convirtieran en expresiones PHP válidas. Su propósito principal era crear elementos HTML personalizados y reutilizables.

    El principio fundamental de esta extensión era hacer que el código front-end fuera más fácil de entender y ayudar a evitar ataques de cross-site scripting. El proyecto tuvo éxito en prevenir el contenido malicioso enviado por el usuario.

    Pero había un problema diferente con XHP: las aplicaciones web dinámicas requieren muchas idas y vueltas al servidor, y XHP no resolvía este problema. Además, toda la interfaz de usuario se volvía a renderizar por pequeños cambios en la aplicación. Más tarde, se creó el prototipo inicial de React con el nombre **FaxJS** por Jordan, inspirado en XHP. Finalmente, después de algún tiempo, React se introdujo como una nueva biblioteca en el mundo de JavaScript.

    **Nota:** JSX proviene de la idea de XHP.

### 3. ¿Cuáles son las principales características de React?

    Las principales características de React son:

    - Utiliza sintaxis **JSX**, una extensión de JS que permite a los desarrolladores escribir HTML en su código JavaScript.
    - Usa **Virtual DOM** en lugar del DOM real, considerando que las manipulaciones del DOM real son costosas.
    - Soporta **renderizado del lado del servidor**, útil para optimización de motores de búsqueda (SEO).
    - Sigue un flujo de datos **unidireccional** (one-way data flow o data binding).
    - Utiliza componentes de UI **reutilizables/componibles** para desarrollar la vista.

### 4. ¿Qué es JSX?

    _JSX_ significa _JavaScript XML_ y es una extensión de sintaxis similar a XML para ECMAScript. Básicamente, proporciona azúcar sintáctico para la función `React.createElement(type, props, ...children)`, dándonos la expresividad de JavaScript junto con una sintaxis de plantilla similar a HTML.

    En el ejemplo siguiente, el texto dentro de la etiqueta `<h1>` se devuelve como una función JavaScript a la función render.

    ```jsx harmony
    export default function App() {
      return <h1 className="greeting">{"¡Hola, esto es código JSX!"}</h1>;
    }
    ```

    Si no usas la sintaxis JSX, el código JavaScript equivalente sería:

    ```javascript
    import { createElement } from "react";

    export default function App() {
      return createElement(
        "h1",
        { className: "greeting" },
        "¡Hola, esto es código JSX!"
      );
    }
    ```

     <details><summary><b>Ver Clase</b></summary>
     <p>

    ```jsx harmony
    class App extends React.Component {
      render() {
        return <h1 className="greeting">{"¡Hola, esto es código JSX!"}</h1>;
      }
    }
    ```

     </p>
     </details>

    **Nota:** JSX es más estricto que HTML.

### 5. ¿Cuál es la diferencia entre un Elemento y un Componente?

    **Elemento:**

    - Un **Elemento** de React es un objeto plano de JavaScript que describe lo que quieres ver en la UI. Representa un nodo DOM o un componente en un momento específico.
    - Los elementos son inmutables: una vez creados, no puedes cambiar sus propiedades. En su lugar, creas nuevos elementos para reflejar actualizaciones.
    - Los elementos pueden anidarse dentro de otros elementos a través de sus `props`.
    - Crear un elemento es una operación rápida y ligera; **no** crea nodos DOM reales ni renderiza nada directamente en la pantalla.

      **Ejemplo (sin JSX):**

      ```js
      const element = React.createElement(
        "button",
        { id: "login-btn" },
        "Iniciar sesión"
      );
      ```

      **Sintaxis JSX equivalente:**

      ```jsx
      <button id="login-btn">Iniciar sesión</button>
      ```

      **El objeto devuelto por `React.createElement`:**

      ```js
      {
        type: 'button',
        props: {
          id: 'login-btn',
          children: 'Iniciar sesión'
        }
      }
      ```

      Los elementos luego se pasan al renderizador de React DOM (por ejemplo, `ReactDOM.render()`), que los traduce a nodos DOM reales.

      ***

    **Componente:**

    - Un **Componente** es una función o clase que devuelve un elemento (o un árbol de elementos) para describir parte de la UI. Los componentes pueden aceptar entradas (llamadas **props**) y gestionar su propio estado (en el caso de componentes de clase o funciones con hooks).
    - Los componentes permiten dividir la UI en partes independientes y reutilizables, cada una aislada y componible.
    - Puedes definir un componente usando una función o una clase:

      **Ejemplo (Componente de Función con JSX):**

      ```jsx
      const Button = ({ handleLogin }) => (
        <button id="login-btn" onClick={handleLogin}>
          Iniciar sesión
        </button>
      );
      ```

      Cuando se compila JSX, se transforma en un árbol de llamadas a `React.createElement`:

      ```js
      const Button = ({ handleLogin }) =>
        React.createElement(
          "button",
          { id: "login-btn", onClick: handleLogin },
          "Iniciar sesión"
        );
      ```

      ***

    **En resumen:**

    - **Elementos** son los bloques más pequeños en React: objetos que describen lo que quieres ver.
    - **Componentes** son funciones o clases que devuelven elementos y encapsulan lógica, estructura y comportamiento para partes de tu UI.

    > Piensa en los **elementos** como las instrucciones para crear la UI, y en los **componentes** como planos reutilizables que combinan lógica y estructura para generar esas instrucciones.

### 6. ¿Cómo se crean componentes en React?

    Los componentes son los bloques de construcción para crear interfaces de usuario (UI) en React. Hay dos formas posibles de crear un componente.

    1. **Componentes de Función:** Esta es la forma más simple de crear un componente. Son funciones puras de JavaScript que aceptan un objeto de props como único parámetro y devuelven elementos React para renderizar la salida:

       ```jsx harmony
       function Saludo({ mensaje }) {
         return <h1>{`Hola, ${mensaje}`}</h1>;
       }
       ```

    2. **Componentes de Clase:** También puedes usar una clase ES6 para definir un componente. El componente de función anterior se puede escribir como un componente de clase:

       ```jsx harmony
       class Saludo extends React.Component {
         render() {
           return <h1>{`Hola, ${this.props.mensaje}`}</h1>;
         }
       }
       ```

### 7. ¿Cuándo usar un Componente de Clase en lugar de un Componente de Función?

    Después de la adición de Hooks (es decir, desde React 16.8 en adelante), se recomienda siempre usar componentes de función en lugar de componentes de clase en React. Porque puedes usar estado, métodos de ciclo de vida y otras características que antes solo estaban disponibles en componentes de clase, ahora también en componentes de función.

    Pero aún hay dos razones para usar componentes de clase sobre componentes de función:

    1. Si necesitas una funcionalidad de React cuyo equivalente en componentes de función aún no existe, como Límites de Error (Error Boundaries).
    2. En versiones antiguas, si el componente necesita _estado o métodos de ciclo de vida_, entonces necesitas usar un componente de clase.

    Así que el resumen de esta pregunta es el siguiente:

    **Usa Componentes de Función:**

    - Si no necesitas estado o métodos de ciclo de vida, y tu componente es puramente presentacional.
    - Por simplicidad, legibilidad y prácticas modernas de código, especialmente con el uso de React Hooks para estado y efectos secundarios.

    **Usa Componentes de Clase:**

    - Si necesitas gestionar estado o usar métodos de ciclo de vida.
    - En escenarios donde sea necesaria la compatibilidad con versiones anteriores o la integración con código antiguo.

    **Nota:** También puedes usar componentes reutilizables de [límite de error de React](https://github.com/bvaughn/react-error-boundary) de terceros sin escribir ninguna clase. Es decir, no es necesario usar componentes de clase para Límites de Error.

    El uso de Límites de Error de la biblioteca anterior es bastante sencillo.

    > **_Nota al usar react-error-boundary:_** ErrorBoundary es un componente de cliente. Solo puedes pasarle props que sean serializables o usarlo en archivos que tengan una directiva `"use client";`.

    ```jsx
    "use client";

    import { ErrorBoundary } from "react-error-boundary";

    <ErrorBoundary fallback={<div>Algo salió mal</div>}>
      <ExampleApplication />
    </ErrorBoundary>;
    ```

### 8. ¿Qué son los Componentes Puros?

    Los componentes puros son aquellos que renderizan la misma salida para el mismo estado y props. En componentes de función, puedes lograr estos componentes puros mediante la API memoizada `React.memo()` que envuelve al componente. Esta API evita renderizados innecesarios comparando los props anteriores y nuevos usando una comparación superficial. Por lo tanto, será útil para optimizaciones de rendimiento.

    Pero al mismo tiempo, no compara el estado anterior con el estado actual porque el componente de función en sí mismo evita el renderizado innecesario por defecto cuando estableces el mismo estado nuevamente.

    La representación sintáctica de los componentes memoizados se ve así:

    ```jsx
    const ComponenteMemoizado = memo(AlgunComponente, sonPropsIguales?);
    ```

    A continuación, un ejemplo de cómo un componente hijo (por ejemplo, PerfilEmpleado) evita renderizados para los mismos props pasados por el componente padre (por ejemplo, FormularioRegistroEmpleado).

    ```jsx
    import { memo, useState } from "react";

    const PerfilEmpleado = memo(function PerfilEmpleado({ nombre, email }) {
      return (
        <>
          <p>Nombre: {nombre}</p>
          <p>Email: {email}</p>
        </>
      );
    });
    export default function FormularioRegistroEmpleado() {
      const [nombre, setNombre] = useState("");
      const [email, setEmail] = useState("");
      return (
        <>
          <label>
            Nombre:{" "}
            <input value={nombre} onChange={(e) => setNombre(e.target.value)} />
          </label>
          <label>
            Email:{" "}
            <input value={email} onChange={(e) => setEmail(e.target.value)} />
          </label>
          <hr />
          <PerfilEmpleado nombre={nombre} />
        </>
      );
    }
    ```

    En el código anterior, el prop `email` no se ha pasado al componente hijo. Por lo tanto, no habrá re-renderizados por cambios en el prop `email`.

    En componentes de clase, los componentes que extienden _`React.PureComponent`_ en lugar de _`React.Component`_ se convierten en componentes puros. Cuando los props o el estado cambian, _PureComponent_ hace una comparación superficial tanto de props como de estado invocando el método del ciclo de vida `shouldComponentUpdate()`.

    **Nota:** `React.memo()` es un componente de orden superior.

### 9. ¿Qué es el estado en React?

    El _estado_ de un componente es un objeto que contiene información que puede cambiar durante la vida del componente. El punto importante es que cada vez que el objeto de estado cambia, el componente se vuelve a renderizar. Siempre se recomienda hacer que nuestro estado sea lo más simple posible y minimizar el número de componentes con estado.

    ![state](images/state.jpg)

    Tomemos un ejemplo del componente **Usuario** con el estado `mensaje`. Aquí, se ha utilizado el hook **useState** para agregar estado al componente Usuario y devuelve un array con el estado actual y una función para actualizarlo.

    ```jsx harmony
    import { useState } from "react";

    function Usuario() {
      const [mensaje, setMensaje] = useState("Bienvenido al mundo de React");

      return (
        <div>
          <h1>{mensaje}</h1>
        </div>
      );
    }
    ```

    Cada vez que React llama a tu componente o accede al hook `useState`, te da una instantánea del estado para ese renderizado particular.

    <details><summary><b>Ver Clase</b></summary>
    <p>

    ```jsx harmony
    import React from "react";
    class Usuario extends React.Component {
      constructor(props) {
        super(props);

        this.state = {
          mensaje: "Bienvenido al mundo de React",
        };
      }

      render() {
        return (
          <div>
            <h1>{this.state.mensaje}</h1>
          </div>
        );
      }
    }
    ```

    </p>
    </details>

    El estado es similar a los props, pero es privado y completamente controlado por el componente, es decir, no es accesible para ningún otro componente hasta que el componente propietario decida pasarlo.

### 10. ¿Qué son los props en React?

    _Props_ son entradas para componentes. Son valores individuales u objetos que contienen un conjunto de valores pasados a componentes al crearlos (similares a atributos HTML). Los datos fluyen desde componentes padres a hijos.

    **Propósito:**

    1. Pasar datos personalizados
    2. Activar cambios de estado
    3. Acceder via `this.props.propReact` en componentes de clase

    **Ejemplo:**

    ```jsx
    <Elemento reactProp={"valor"} />
    ```

    **Componente funcional:**

    ```jsx
    const Hijo = (
      { nombre, edad = 25 } // Valor por defecto
    ) => (
      <div>
        {nombre} - {edad}
      </div>
    );
    ```

    **Componente de clase:**

    ```jsx
    class Hijo extends React.Component {
      render() {
        return <div>{this.props.nombre}</div>;
      }
    }
    ```

    **Nota:** Los props son inmutables (no pueden modificarse por el componente hijo).

### 11. ¿Cuál es la diferencia entre `state` y `props`?

    **State**:

    - Es un objeto interno del componente que contiene datos que pueden cambiar con el tiempo.
    - Es **mutable**.
    - Es **privado** y local al componente.
    - Se actualiza con `setState` (en clases) o `useState` (en funciones).
    - Cambiar el estado dispara un **re-render** del componente.

    **Props**:

    - Son valores que un componente **padre pasa a un hijo**.
    - Son **inmutables** desde el punto de vista del componente hijo.
    - Permiten configurar y reutilizar componentes.
    - No pueden ser modificadas por el componente que las recibe.

    | Característica    | `state`                   | `props`                          |
    | ----------------- | ------------------------- | -------------------------------- |
    | Quién lo gestiona | El propio componente      | El componente padre              |
    | ¿Mutable?         | Sí                        | No (solo lectura)                |
    | Alcance           | Local                     | Externo, recibido desde el padre |
    | Propósito         | Manejo de datos dinámicos | Personalizar componentes         |
    | Cómo se actualiza | `setState` o `useState`   | No se actualiza internamente     |

    ---   

### 12. ¿Cuál es la diferencia entre manejo de eventos en HTML y en React?

    - En HTML se usan atributos en minúsculas (`onclick`), en React se usa camelCase (`onClick`).
    - En HTML se puede retornar `false` para evitar el comportamiento por defecto; en React se debe usar `event.preventDefault()`.
    - En React no se llama directamente la función con paréntesis: se pasa la **referencia**.

    ```jsx
    <button onClick={activarLaser}>Disparar</button>
    ```

    ---

    ### 13. ¿Qué son los Synthetic Events en React?

Son una abstracción que React crea para normalizar el comportamiento de eventos en diferentes navegadores. Proveen una API consistente y tienen métodos como `stopPropagation()` y `preventDefault()`. Aun así, podés acceder al evento nativo con `event.nativeEvent`.

---

### 14. ¿Qué son las expresiones condicionales inline?

    Podés usar operadores ternarios o lógicos para renderizar JSX condicionalmente dentro del `return`.

    ```jsx
    {
    mensajes.length > 0 && <p>Tienes {mensajes.length} mensajes nuevos.</p>;
    }
    ```

    También podés usar ternarios:

    ```jsx
    {
    isLoggedIn ? <Dashboard /> : <Login />;
    }
    ```

    ---

### 15. ¿Qué es la `key` en un array de elementos y por qué es importante?

    - La prop `key` ayuda a React a identificar qué ítems en una lista cambiaron, se agregaron o se eliminaron.
    - Deben ser **únicas** entre los hermanos.
    - Evitá usar índices como `key` salvo que el orden nunca cambie.

    ```jsx
    {
    tareas.map((t) => <li key={t.id}>{t.texto}</li>);
    }
    ```

    ---

### 16. ¿Qué es el Virtual DOM?

    Es una representación **en memoria** del DOM real. React renderiza primero en el Virtual DOM, calcula las diferencias (diffing) y actualiza **solo lo necesario** en el DOM real. Este proceso se llama reconciliación.

    ---

### 17. ¿Cómo funciona el Virtual DOM?

    1. Se renderiza una nueva versión del árbol en el Virtual DOM.
    2. Se compara con la versión anterior.
    3. Se actualiza **solo lo que cambió** en el DOM real.

    ---

### 18. ¿Cuál es la diferencia entre Shadow DOM y Virtual DOM?

    - **Shadow DOM**: Especificación de los navegadores para encapsular estilos y estructura dentro de un Web Component.
    - **Virtual DOM**: Es una técnica de React y otras libs para mejorar performance de updates del DOM.

    ---

### 19. ¿Qué es React Fiber?

    Es el nuevo motor de reconciliación de React (desde v16). Permite:

    - Interrumpir renders largos.
    - Asignar prioridad a tareas.
    - Mejorar animaciones y gestos.
    - Hacer rendering incremental.

    ---

### 20. ¿Cuál es el objetivo principal de React Fiber?

    Permitir renderizado **incremental y asíncrono**:

    - Dividir trabajo en chunks.
    - Pausar y reanudar tareas.
    - Asignar prioridades.
    - Soportar mejor los límites de error y múltiples elementos por render.
