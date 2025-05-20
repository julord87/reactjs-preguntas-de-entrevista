# 🧠 Preguntas de Entrevista sobre React - Traducción al Español

## 🧩 Core React

## React Básico

1.  ### ¿Qué es React?

    React (también conocido como React.js o ReactJS) es una **biblioteca JavaScript de front-end de código abierto** que se utiliza para construir interfaces de usuario componibles, especialmente para aplicaciones de una sola página (SPA). Se encarga de la capa de vista en aplicaciones web y móviles basadas en componentes utilizando un enfoque declarativo.

    React fue creado por [Jordan Walke](https://github.com/jordwalke), un ingeniero de software que trabajaba en Facebook. React se implementó por primera vez en el News Feed de Facebook en 2011 y en Instagram en 2012.

    ---

2.  ### ¿Cuál es la historia detrás de la evolución de React?

    La historia de ReactJS comenzó en 2010 con la creación de **XHP**. XHP es una extensión de PHP que mejoró la sintaxis del lenguaje de modo que los fragmentos de documentos XML se convirtieran en expresiones PHP válidas. Su propósito principal era crear elementos HTML personalizados y reutilizables.

    El principio fundamental de esta extensión era hacer que el código front-end fuera más fácil de entender y ayudar a evitar ataques de cross-site scripting. El proyecto tuvo éxito en prevenir el contenido malicioso enviado por el usuario.

    Pero había un problema diferente con XHP: las aplicaciones web dinámicas requieren muchas idas y vueltas al servidor, y XHP no resolvía este problema. Además, toda la interfaz de usuario se volvía a renderizar por pequeños cambios en la aplicación. Más tarde, se creó el prototipo inicial de React con el nombre **FaxJS** por Jordan, inspirado en XHP. Finalmente, después de algún tiempo, React se introdujo como una nueva biblioteca en el mundo de JavaScript.

    **Nota:** JSX proviene de la idea de XHP.

    ---

3.  ### ¿Cuáles son las principales características de React?

    Las principales características de React son:

    - Utiliza sintaxis **JSX**, una extensión de JS que permite a los desarrolladores escribir HTML en su código JavaScript.
    - Usa **Virtual DOM** en lugar del DOM real, considerando que las manipulaciones del DOM real son costosas.
    - Soporta **renderizado del lado del servidor**, útil para optimización de motores de búsqueda (SEO).
    - Sigue un flujo de datos **unidireccional** (one-way data flow o data binding).
    - Utiliza componentes de UI **reutilizables/componibles** para desarrollar la vista.

    ---

4.  ### ¿Qué es JSX?

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

    ---

5.  ### ¿Cuál es la diferencia entre un Elemento y un Componente?

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

    ---

6.  ### ¿Cómo se crean componentes en React?

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
    
    ---

7.  ### ¿Cuándo usar un Componente de Clase en lugar de un Componente de Función?

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

    ---

8.  ### ¿Qué son los Componentes Puros?

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

    ---

9.  ### ¿Qué es el estado en React?

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

    ---

10. ### ¿Qué son los props en React?

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

    ---

11. ### ¿Cuál es la diferencia entre `state` y `props`?

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

12. ### ¿Cuál es la diferencia entre manejo de eventos en HTML y en React?

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

14. ### ¿Qué son las expresiones condicionales inline?

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

15. ### ¿Qué es la `key` en un array de elementos y por qué es importante?

    - La prop `key` ayuda a React a identificar qué ítems en una lista cambiaron, se agregaron o se eliminaron.
    - Deben ser **únicas** entre los hermanos.
    - Evitá usar índices como `key` salvo que el orden nunca cambie.

    ```jsx
    {
    tareas.map((t) => <li key={t.id}>{t.texto}</li>);
    }
    ```

    ---

16. ### ¿Qué es el Virtual DOM?

    Es una representación **en memoria** del DOM real. React renderiza primero en el Virtual DOM, calcula las diferencias (diffing) y actualiza **solo lo necesario** en el DOM real. Este proceso se llama reconciliación.

    ---

17. ### ¿Cómo funciona el Virtual DOM?

    1. Se renderiza una nueva versión del árbol en el Virtual DOM.
    2. Se compara con la versión anterior.
    3. Se actualiza **solo lo que cambió** en el DOM real.

    ---

18. ### ¿Cuál es la diferencia entre Shadow DOM y Virtual DOM?

    - **Shadow DOM**: Especificación de los navegadores para encapsular estilos y estructura dentro de un Web Component.
    - **Virtual DOM**: Es una técnica de React y otras libs para mejorar performance de updates del DOM.

    ---

19. ### ¿Qué es React Fiber?

    Es el nuevo motor de reconciliación de React (desde v16). Permite:

    - Interrumpir renders largos.
    - Asignar prioridad a tareas.
    - Mejorar animaciones y gestos.
    - Hacer rendering incremental.

    ---

20. ### ¿Cuál es el objetivo principal de React Fiber?

    Permitir renderizado **incremental y asíncrono**:

    - Dividir trabajo en chunks.
    - Pausar y reanudar tareas.
    - Asignar prioridades.
    - Soportar mejor los límites de error y múltiples elementos por render.

    ---

21. ### ¿Qué son los componentes controlados?

    Un componente controlado es aquel que maneja sus propios inputs a través del estado de React. Cada cambio en el input se gestiona mediante un handler, y el estado refleja siempre lo que se ve en pantalla.

    Pasos para implementarlo:
    1. Inicializar el estado con `useState`.
    2. Asignar `value={estado}` al input.
    3. Crear una función para manejar cambios.
    4. Vincular esa función con `onChange`.

    ```jsx
    function UserProfile() {
    const [username, setUsername] = useState("");

    const handleChange = (e) => setUsername(e.target.value);

    return (
        <form>
        <label>
            Nombre:
            <input type="text" value={username} onChange={handleChange} />
        </label>
        </form>
    );
    }
    ```

    ---

22. ### ¿Qué son los componentes no controlados?
    Son inputs cuyo valor no está ligado al estado de React, sino que se accede directamente al DOM usando `ref`, como en HTML tradicional.

    Pasos:
    1. Crear un ref con `useRef()`.
    2. Asignarlo al input.
    3. Leer el valor con `.current.value` al enviar el formulario.

    ```jsx
    function UserProfile() {
    const usernameRef = useRef(null);

    const handleSubmit = (e) => {
        e.preventDefault();
        console.log("Username:", usernameRef.current.value);
    };

    return (
        <form onSubmit={handleSubmit}>
        <label>
            Nombre:
            <input type="text" ref={usernameRef} />
        </label>
        <button type="submit">Enviar</button>
        </form>
    );
    }
    ```

    ---

23. ### ¿Cuál es la diferencia entre `createElement` y `cloneElement`?

    - `React.createElement()` se usa para crear nuevos elementos desde cero (lo que hace JSX internamente).
    - `React.cloneElement()` se usa para **copiar** un elemento y pasarle nuevas props.

    ---

24. ### ¿Qué es "Lifting State Up"?

    Cuando dos o más componentes necesitan compartir datos, el estado se "eleva" a su ancestro común más cercano. De esta forma, se centraliza el control y se reparten los datos por props.

    ---

25. ### ¿Qué son los Higher-Order Components (HOC)?

    Un HOC es una función que recibe un componente y retorna uno nuevo, con lógica adicional. Se usa para reutilizar comportamiento sin duplicar código.

    ```js
    const Enhanced = withLogging(Original);
    ```

    Casos de uso:
    - Reutilización de lógica.
    - Hijacking de renderizado.
    - Manipulación de props o estado.

    ---

26. ### ¿Qué es la prop `children`?

    Es una prop especial que permite pasar contenido hijo entre las etiquetas de un componente.

    ```jsx
    function Layout({ children }) {
    return <main>{children}</main>;
    }

    <Layout>
    <h1>Hola</h1>
    </Layout>
    ```

    ---

27. ### ¿Cómo se escriben comentarios en JSX?

    Dentro del JSX, los comentarios se escriben con llaves `{}` y `/* */`:

    ```jsx
    <div>
    {/* Comentario en línea */}
    </div>
    ```

    ---

28. ### ¿Qué es la reconciliación?

    Es el proceso por el cual React compara el Virtual DOM con su versión anterior para aplicar solo los cambios necesarios al DOM real. Esto optimiza el renderizado y mejora la performance.

    ---

29. ### ¿`React.lazy()` permite imports con exports nombrados?

    No. `React.lazy()` solo admite imports por `default`. Para importar un export nombrado, hay que crear un archivo intermedio que lo exporte como default.

    ```js
    // Intermediate.js
    export { NamedComponent as default } from "./Original";
    ```

    ---

30. ### ¿Por qué React usa `className` en lugar de `class`?

    Porque `class` es una palabra reservada en JavaScript. JSX es sintaxis JavaScript, por lo tanto, se usa `className` para asignar clases CSS.

    ---

31. ### ¿Qué son los Fragments?

    Los Fragments permiten agrupar múltiples elementos sin agregar nodos extra al DOM. Se usan con `<Fragment>` o la sintaxis corta `<></>`.

    ```jsx
    function Story({ title, description, date }) {
      return (
        <>
          <h2>{title}</h2>
          <p>{description}</p>
          <p>{date}</p>
        </>
      );
    }
    ```

    También se pueden usar Fragments con `key` al renderizar listas:

    ```jsx
    function StoryBook() {
      return stories.map((story) => (
        <Fragment key={story.id}>
          <h2>{story.title}</h2>
          <p>{story.description}</p>
          <p>{story.date}</p>
        </Fragment>
      ));
    }
    ```

    ---

32. ### ¿Por qué es mejor usar Fragments que divs contenedores?

    - Son más rápidos y consumen menos memoria (no generan nodos extra).
    - Evitan romper diseños con CSS Grid o Flexbox.
    - El DOM queda más limpio.

    ---

33. ### ¿Qué son los Portals en React?

    Permiten renderizar elementos fuera del DOM padre. Se usa para overlays, modals o tooltips.

    ```js
    ReactDOM.createPortal(child, container);
    ```

    El primer argumento es el componente a renderizar, el segundo es un nodo del DOM donde insertarlo.

    ---

34. ### ¿Qué son los componentes sin estado (stateless)?

    Son componentes cuya salida depende solo de las `props`, no del estado interno. Se implementan con funciones simples y no usan hooks ni métodos de ciclo de vida.

    ---

35. ### ¿Qué son los componentes con estado (stateful)?

    Son aquellos que manejan su propio estado interno con `useState` o `this.state`.

    ```jsx
    const App = () => {
      const [count, setCount] = useState(0);
      const handleIncrement = () => setCount(count + 1);

      return (
        <>
          <button onClick={handleIncrement}>Incrementar</button>
          <span>Contador: {count}</span>
        </>
      );
    };
    ```

    ---

36. ### ¿Cómo validar `props` en React?

    Se usa la librería `prop-types`. En desarrollo, React lanza advertencias si las `props` no coinciden con lo esperado.

    ```js
    import PropTypes from "prop-types";

    function User({ name, age }) {
      return (
        <>
          <h1>Bienvenido, {name}</h1>
          <h2>Edad: {age}</h2>
        </>
      );
    }

    User.propTypes = {
      name: PropTypes.string.isRequired,
      age: PropTypes.number.isRequired,
    };
    ```

    ---

37. ### ¿Cuáles son las ventajas de React?

    - Virtual DOM mejora la performance.
    - JSX es legible y expresivo.
    - SSR y CSR.
    - Fácil integración con otros frameworks.
    - Testeo sencillo con Jest.

    ---

38. ### ¿Y sus limitaciones?

    - No es un framework completo.
    - Curva de aprendizaje inicial.
    - Integración con MVC requiere configuración.
    - JSX puede parecer complejo al inicio.
    - Muchos componentes pequeños pueden generar sobreingeniería.

    ---

39. ### ¿Cómo se recomienda hacer type checking?

    - Para proyectos chicos: `prop-types`.
    - Para proyectos grandes: usar Flow o TypeScript, que validan tipos en tiempo de compilación y ofrecen autocompletado.

    ---

40. ### ¿Para qué sirve el paquete `react-dom`?

    Provee funciones específicas del DOM para usar al tope de la app:

    - `render()`
    - `hydrate()`
    - `unmountComponentAtNode()`
    - `findDOMNode()`
    - `createPortal()`

    ---

41. ### ¿Qué es `ReactDOMServer`?

    El objeto `ReactDOMServer` permite renderizar componentes a HTML estático, normalmente desde un servidor Node (SSR - Server Side Rendering).

    Métodos principales:
    - `renderToString()`
    - `renderToStaticMarkup()`

    Ejemplo con Express:

    ```js
    import { renderToString } from "react-dom/server";
    import MyPage from "./MyPage";

    app.get("/", (req, res) => {
      res.write("<!DOCTYPE html><html><head><title>My Page</title></head><body>");
      res.write('<div id="content">');
      res.write(renderToString(<MyPage />));
      res.write("</div></body></html>");
      res.end();
    });
    ```

    ---

42. ### ¿Cómo se usa `innerHTML` en React?

    En React se usa `dangerouslySetInnerHTML` en lugar de `innerHTML`. Es una forma insegura de inyectar HTML directamente, por lo que debe usarse con cuidado.

    ```jsx
    function createMarkup() {
      return { __html: "Primero &middot; Segundo" };
    }

    function MyComponent() {
      return <div dangerouslySetInnerHTML={createMarkup()} />;
    }
    ```

    ---

43. ### ¿Cómo se aplican estilos en línea en React?

    Se usa la prop `style`, que recibe un objeto JS con nombres de propiedad en camelCase:

    ```jsx
    const divStyle = {
      color: "blue",
      backgroundImage: "url(" + imgUrl + ")",
    };

    function HelloWorldComponent() {
      return <div style={divStyle}>¡Hola Mundo!</div>;
    }
    ```

    ---

44. ### ¿Cómo se manejan eventos en React?

    - Los nombres de eventos se escriben en camelCase (`onClick`).
    - Se pasan funciones, no strings.

    ```jsx
    <button onClick={handleClick}>Clickeame</button>
    ```

    ---

45. ### ¿Cuál es el impacto de usar índices como `key`?

    Usar índices como `key` puede generar bugs y dificultar la optimización de React.

    Mal ejemplo (con índice):
    ```jsx
    todos.map((todo, index) => <Todo {...todo} key={index} />);
    ```

    Buen ejemplo (con id estable):
    ```jsx
    todos.map((todo) => <Todo {...todo} key={todo.id} />);
    ```

    ---

46. ### ¿Cómo renderizar condicionalmente componentes?

    Se puede usar el operador lógico `&&` o un ternario.

    ```jsx
    {isLoggedIn && <Dashboard />}

    {hasAddress
      ? <p>{address}</p>
      : <p>Dirección no disponible</p>}
    ```

    ---

47. ### ¿Por qué hay que tener cuidado al hacer `spread` de props?

    Al hacer `...props` se puede inyectar atributos no válidos al DOM. Es mejor desestructurar y usar `...rest` sólo donde haga falta.

    ```jsx
    const ComponentB = ({ isVisible, ...domProps }) => (
      <div {...domProps}>Contenido</div>
    );
    ```

    ---

48. ### ¿Cómo se memoiza un componente?

    Desde React 16.6 se puede usar `React.memo()` para evitar renders innecesarios si las props no cambian.

    ```jsx
    const MemoComponent = React.memo(function MemoComponent(props) {
      return <div>{props.texto}</div>;
    });
    ```

    También se puede usar una lib como `moize`:

    ```jsx
    import moize from "moize";
    const MemoizedFoo = moize.react(MyComponent);
    ```

    ---

49. ### ¿Cómo se implementa SSR (Server-Side Rendering)?

    React permite renderizar en el servidor con `react-dom/server`:

    ```js
    import ReactDOMServer from "react-dom/server";
    import App from "./App";

    const html = ReactDOMServer.renderToString(<App />);
    ```

    Luego se inserta ese HTML en el documento para enviarlo al cliente.

    ---

50. ### ¿Para qué sirve el paquete `react-dom`?

    Contiene métodos específicos para manipular el DOM:

    - `render()` — Renderiza el componente en el DOM.
    - `hydrate()` — Similar a render, pero hidrata markup generado por SSR.
    - `unmountComponentAtNode()` — Quita un componente del DOM.
    - `findDOMNode()` — Accede al nodo DOM de un componente (deprecated en strict mode).
    - `createPortal()` — Renderiza fuera del árbol padre.

    ---

51. ### ¿Los Hooks reemplazan a los render props y los HOC (higher-order components)?

    En muchos casos sí. Los Hooks permiten reutilizar lógica sin anidar componentes como ocurre con render props o HOC, reduciendo el árbol de componentes y mejorando la legibilidad.

    ---

52. ### ¿Qué es un componente de switching?

    Es un componente que renderiza distintos componentes hijos según una prop determinada.

    ```jsx
    import HomePage from "./HomePage";
    import AboutPage from "./AboutPage";
    import ServicesPage from "./ServicesPage";
    import ContactPage from "./ContactPage";

    const PAGES = {
      home: HomePage,
      about: AboutPage,
      services: ServicesPage,
      contact: ContactPage,
    };

    const Page = (props) => {
      const Handler = PAGES[props.page] || ContactPage;
      return <Handler {...props} />;
    };

    Page.propTypes = {
      page: PropTypes.oneOf(Object.keys(PAGES)).isRequired,
    };
    ```

    ---

53. ### ¿Qué son los Mixins en React?

    Eran una forma de compartir lógica entre componentes en React clásico (`createClass`). Hoy están **obsoletos** y reemplazados por HOC o Hooks.

    Ejemplo (no recomendado):

    ```js
    const PureRenderMixin = require("react-addons-pure-render-mixin");

    const Button = React.createClass({
      mixins: [PureRenderMixin],
      // ...
    });
    ```

    ---

54. ### ¿Qué eventos Pointer soporta React?

    React soporta los eventos Pointer que unifican mouse, touch y stylus:

    - `onPointerDown`
    - `onPointerMove`
    - `onPointerUp`
    - `onPointerCancel`
    - `onGotPointerCapture`
    - `onLostPointerCapture`
    - `onPointerEnter`
    - `onPointerLeave`
    - `onPointerOver`
    - `onPointerOut`

    ---

55. ### ¿Por qué los nombres de componentes deben comenzar con mayúscula?

    En JSX, los nombres que empiezan con minúscula se interpretan como etiquetas HTML. Por eso los componentes deben tener nombres en mayúscula:

    ```jsx
    function MiComponente() { ... }
    ```

    Incluso si se exporta con minúscula, debe importarse con mayúscula para que React lo reconozca como componente:

    ```jsx
    import MiComponente from './miComponente';
    ```

    ---

56. ### ¿React v16 admite atributos DOM personalizados?

    Sí. A diferencia de versiones anteriores, ahora React conserva los atributos desconocidos en el DOM:

    ```jsx
    <div miatributo="valor" />
    ```

    Esto permite probar nuevas APIs del DOM o integrarse con librerías externas.

    ---

57. ### ¿Cómo hacer loops en JSX?

    Usá `.map()`:

    ```jsx
    <ul>
      {items.map((item) => (
        <li key={item.id}>{item.nombre}</li>
      ))}
    </ul>
    ```

    No podés usar `for` directamente dentro de JSX porque no es una expresión.

    ---

58. ### ¿Cómo acceder a props dentro de comillas en JSX?

    JSX no permite interpolación dentro de strings:

    ❌ Incorrecto:
    ```jsx
    <img src="images/{props.image}" />
    ```

    ✅ Correcto:
    ```jsx
    <img src={"images/" + props.image} />
    // o usando template strings:
    <img src={`images/${props.image}`} />
    ```

    ---

59. ### ¿Qué es un PropType array con shape?

    Permite validar un array de objetos con estructura definida:

    ```js
    MyComponent.propTypes = {
      items: PropTypes.arrayOf(
        PropTypes.shape({
          color: PropTypes.string.isRequired,
          fontSize: PropTypes.number.isRequired,
        })
      ).isRequired,
    };
    ```

    ---

60. ### ¿Cómo aplicar clases condicionales en JSX?

    No se puede usar `{}` dentro de `""`:

    ❌ Incorrecto:
    ```jsx
    <div className="box {isActive ? 'on' : 'off'}" />
    ```

    ✅ Correcto:
    ```jsx
    <div className={'box ' + (isActive ? 'on' : 'off')} />
    // o con template strings
    <div className={`box ${isActive ? 'on' : 'off'}`} />
    ```

    ---

61. ### ¿Cuál es la diferencia entre `react` y `react-dom`?

    El paquete `react` incluye funciones como `React.createElement()`, `React.Component`, `React.Children`, y otros helpers para crear y gestionar componentes. Estas herramientas son universales (isomorphic) y se usan tanto en el cliente como en el servidor.

    El paquete `react-dom` incluye funciones específicas del DOM como `ReactDOM.render()` y, en su versión de servidor (`react-dom/server`), incluye `ReactDOMServer.renderToString()` y `renderToStaticMarkup()` para renderizado del lado del servidor (SSR).

    ---

62. ### ¿Por qué se separó `react-dom` de `react`?

    A partir de la versión 0.14, React separó la lógica del DOM en un paquete independiente: `react-dom`. Esto permitió que React pudiera adaptarse a otros entornos como `react-native`, `react-canvas` o `react-three`.

    Esta separación facilita el uso compartido de componentes entre distintas plataformas (web, móvil, etc.).

    ---

63. ### ¿Cómo usar la etiqueta `label` en React?

    En HTML, la etiqueta `label` utiliza el atributo `for`, pero como `for` es una palabra reservada en JavaScript, React utiliza `htmlFor`.

    ```jsx
    <label htmlFor="usuario">Usuario</label>
    <input id="usuario" type="text" />
    ```

    ---

64. ### ¿Cómo combinar múltiples objetos de estilo en línea?

    En React web se usa el operador _spread_:

    ```jsx
    <button style={{ ...styles.boton, ...styles.submit }}>Enviar</button>
    ```

    En React Native se puede usar un array:

    ```jsx
    <View style={[styles.boton, styles.submit]} />
    ```

    ---

65. ### ¿Cómo volver a renderizar la vista cuando se redimensiona el navegador?

    Usá `useEffect` para escuchar eventos `resize` y `useState` para guardar las dimensiones.

    ```jsx
    import React, { useState, useEffect } from "react";

    function WindowDimensions() {
      const [size, setSize] = useState({
        width: window.innerWidth,
        height: window.innerHeight,
      });

      useEffect(() => {
        const handleResize = () => {
          setSize({ width: window.innerWidth, height: window.innerHeight });
        };

        window.addEventListener("resize", handleResize);
        return () => window.removeEventListener("resize", handleResize);
      }, []);

      return <span>{size.width} x {size.height}</span>;
    }
    ```

    También se puede hacer con componentes de clase usando `componentDidMount` y `componentWillUnmount`.

    ---

66. ### ¿Cómo formatear (pretty print) un JSON en React?

    Usá `JSON.stringify` con el parámetro `null, 2` dentro de un `<pre>`:

    ```jsx
    const data = { nombre: "Juan", edad: 42 };

    function Usuario() {
      return <pre>{JSON.stringify(data, null, 2)}</pre>;
    }
    ```

    También funciona con clases:

    ```jsx
    class Usuario extends React.Component {
      render() {
        return <pre>{JSON.stringify(data, null, 2)}</pre>;
      }
    }
    ```

    ---

67. ### ¿Por qué no se pueden modificar las `props`?

    En React las `props` son **inmutables** y fluyen en un único sentido (de padre a hijo). El componente hijo puede leerlas, pero no modificarlas.

    ---

68. ### ¿Cómo enfocar un input al cargar la página?

    Con `useRef` y `useEffect`:

    ```jsx
    import React, { useRef, useEffect } from "react";

    function App() {
      const inputRef = useRef(null);

      useEffect(() => {
        inputRef.current.focus();
      }, []);

      return (
        <div>
          <input defaultValue="No enfocado" />
          <input ref={inputRef} defaultValue="Enfocado" />
        </div>
      );
    }
    ```

    Con clases, se hace en `componentDidMount` usando una referencia:

    ```jsx
    class App extends React.Component {
      componentDidMount() {
        this.nombreInput.focus();
      }

      render() {
        return (
          <div>
            <input defaultValue="No enfocado" />
            <input
              ref={(input) => (this.nombreInput = input)}
              defaultValue="Enfocado"
            />
          </div>
        );
      }
    }
    ```

    ---

69. ### ¿Cómo obtener la versión de React en tiempo de ejecución?

    Se puede acceder mediante `React.version`:

    ```jsx
    const version = React.version;

    ReactDOM.render(
      <div>{`Versión de React: ${version}`}</div>,
      document.getElementById("app")
    );
    ```

    ---
