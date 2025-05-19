# 🧠 Preguntas de Entrevista sobre React - Traducción al Español

> Traducción realizada por Juliano + ChatGPT a partir del repositorio de [SudheerJonna](https://github.com/sudheerj/reactjs-interview-questions).

## 🧩 Core React - Preguntas 1 a 10

### 1. ¿Qué es React?
React (también conocido como React.js o ReactJS) es una biblioteca de JavaScript de código abierto para construir interfaces de usuario (UI) componibles. Está diseñada especialmente para aplicaciones de una sola página (SPA), manejando la capa de vista de forma declarativa.

### 2. ¿Cuál es la historia detrás de la evolución de React?
React fue creado por Jordan Walke, un ingeniero de software de Facebook. Se inspiró en XHP (una extensión de PHP). React fue usado por primera vez en el News Feed de Facebook en 2011 y en Instagram en 2012.

### 3. ¿Cuáles son las principales características de React?
- JSX: sintaxis que permite escribir HTML dentro de JavaScript.
- Virtual DOM: manipulación eficiente del DOM.
- Renderizado del lado del servidor (SSR).
- Flujo de datos unidireccional.
- Componentes reutilizables y componibles.

### 4. ¿Qué es JSX?
JSX significa JavaScript XML. Es una extensión de sintaxis que permite escribir estructuras HTML en el mismo archivo que el código JavaScript. Por ejemplo:

```jsx
<h1>Hola mundo</h1>
```

equivale a:

```js
React.createElement('h1', null, 'Hola mundo');
```

### 5. ¿Cuál es la diferencia entre un Elemento y un Componente?
- **Elemento**: es un objeto plano que describe lo que se quiere renderizar en pantalla.
- **Componente**: es una función o clase que retorna un elemento o árbol de elementos.

### 6. ¿Cómo se crean componentes en React?
- **Funcionales**: usando funciones que retornan JSX.
- **De clase**: usando clases que extienden `React.Component` y definen un método `render()`.

### 7. ¿Cuándo deberías usar un componente de clase sobre uno funcional?
Hoy en día, con la llegada de los Hooks, se recomienda usar componentes funcionales. Solo en casos como límites de error (`Error Boundaries`) es común seguir usando clases.

### 8. ¿Qué son los componentes puros (Pure Components)?
Son componentes que evitan renders innecesarios. En funciones, se usa `React.memo()`. En clases, se extiende de `React.PureComponent`, que hace una comparación superficial de props y estado.

### 9. ¿Qué es el estado (state) en React?
Es un objeto local del componente que representa datos que pueden cambiar con el tiempo. Al cambiar el estado, React vuelve a renderizar el componente.

### 10. ¿Qué son las props en React?
Las props (propiedades) son datos que se pasan de un componente padre a uno hijo. Son inmutables desde el punto de vista del componente receptor.

---
