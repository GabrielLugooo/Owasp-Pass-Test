<img align="center" src="https://media.licdn.com/dms/image/v2/D4D16AQGUNxQ7NSC05A/profile-displaybackgroundimage-shrink_350_1400/profile-displaybackgroundimage-shrink_350_1400/0/1738695150340?e=1744243200&v=beta&t=oXX-ixT9bR3dJcYCLv4KBs5wjKFoeP0524kFGHQMYmQ" alt="gabriellugo" />

# PRUEBA OWASP DE FUERZA DE CONTRASEÑA

<a href="https://github.com/GabrielLugooo/Owasp-Pass-Test/blob/main/README%20Spanish.md" target="_blank" rel="noreferrer noopener"> <img align="center" src="https://img.shields.io/badge/OWASP%20Español-000000" alt="OWASP Español" /></a>
<a href="https://github.com/GabrielLugooo/Owasp-Pass-Test/tree/main" target="_blank" rel="noreferrer noopener"> <img align="center" src="https://img.shields.io/badge/OWASP%20Inglés-green" alt="OWASP Inglés" /></a>

### Objetivos

OWASP Password Strenght Test es un comprobador de la solidez de contraseñas basado en las <a href="https://cheatsheetseries.owasp.org/cheatsheets/Authentication_Cheat_Sheet.html#Implement_Proper_Password_Strength_Controls" target="_blank" rel="noreferrer noopener">Directrices de OWASP para Contraseñas Seguras</a>. Es liviano, extensible, no tiene dependencias y se puede utilizar en el servidor (nodejs) o en el navegador.

OWASP Password Strenght Test no es un proyecto de OWASP, simplemente se basa en la investigación de OWASP.

### Habilidades Aprendidas

- Comprensión de las pautas de OWASP para autenticación y aplicación de contraseñas.
- Competencia en el análisis e interpretación de node.js, jsno y yaml.
- Capacidad para generar y reconocer firmas y patrones en autenticación, identidad digital, verificación de identidad y gestión de sesiones.
- Conocimiento mejorado de protocolos de red y vulnerabilidades de seguridad.
- Desarrollo de pensamiento crítico y habilidades de resolución de problemas en ciberseguridad.

### Herramientas Usadas

![Static Badge](https://img.shields.io/badge/OWASP-000000?logo=owasp&logoSize=auto)
![Static Badge](https://img.shields.io/badge/HTML-000000?logo=html5&logoSize=auto)
![Static Badge](https://img.shields.io/badge/Javascript-000000?logo=javascript&logoSize=auto)
![Static Badge](https://img.shields.io/badge/Node.JS-000000?logo=nodedotjs&logoSize=auto)
![Static Badge](https://img.shields.io/badge/Json-000000?logo=json&logoSize=auto)
![Static Badge](https://img.shields.io/badge/YAML-000000?logo=yaml&logoSize=auto)
![Static Badge](https://img.shields.io/badge/Travis-000000?logo=travis&logoSize=auto)

### Instalación

- #### Del lado del servidor (node.js)
  Desde la línea de comandos:

```sh
npm install owasp-password-strength-test
```

- #### En el navegador
  Dentro de su documento:

```html
<script src="owasp-password-strength-test.js"></script>
```

### Características

Este módulo se basa en las siguientes creencias:

1. <a href="https://xkcd.com/936/" target="_blank" rel="noreferrer noopener">Las frases de contraseña son mejores que las contraseñas</a>

2. Las contraseñas deben estar sujetas a requisitos de complejidad más estrictos que las frases de contraseña.

Por lo tanto, el módulo:

- **proporciona pruebas "obligatorias" y "opcionales"**.
  Para que una contraseña se considere "segura", debe pasar _todas_ las pruebas requeridas, así como una
  cantidad configurable de pruebas opcionales. Esto permite que siempre se cumplan ciertas reglas (como la longitud mínima de la contraseña), al tiempo que brinda a los usuarios
  la flexibilidad de respetar solo algunas de un conjunto de reglas de menor prioridad.

- **incentiva el uso de frases de contraseña en lugar de contraseñas**.
  Las frases de contraseña (de manera predeterminada) no están sujetas a los mismos requisitos de complejidad que una contraseña.
  (Por lo que, de manera predeterminada, una "frase de contraseña" se puede definir como "una contraseña cuya longitud es mayor o igual a 20 caracteres").

- **se puede extender arbitrariamente**
  Según sea necesario con pruebas adicionales obligatorias y opcionales.

### Uso

Después de haberlo incluido en su proyecto, usar el módulo es sencillo:

- #### Del lado del servidor

```javascript
// require the module
var owasp = require("owasp-password-strength-test");

// invocar test() para probar la solidez de una contraseña
var result = owasp.test("correct horse battery staple");
```

- #### En el navegador

```javascript
// en el navegador, incluir el script hará que un
// objeto `window.owaspPasswordStrengthTest` esté disponible.
var result = owaspPasswordStrengthTest.test("correct horse battery staple");
```

El valor devuelto tendrá esta forma cuando la contraseña sea válida:

```javascript
{
errors : [],
failedTests : [],
requiredTestErrors : [],
optionTestErrors : [],
passedTests : [ 0, 1, 2, 3, 4, 5, 6 ],
isPassphrase : false,
strong : true,
optionTestsPassed : 4
}
```

y tendrá esta forma cuando la contraseña no sea válida:

```javascript
{
errors: [
'La contraseña debe tener al menos 10 caracteres.',
'La contraseña debe contener al menos una letra mayúscula.',
'La contraseña debe contener al menos un número.',
'La contraseña debe contener al menos un carácter especial.'
],
failedTests : [ 0, 4, 5, 6 ],
passedTests : [ 1, 2, 3 ],
requiredTestErrors : [
'La contraseña debe tener al menos 10 caracteres.',
],
optionalTestErrors : [
'La contraseña debe contener al menos una letra mayúscula.',
'La contraseña debe contener al menos un número.',
'La contraseña debe contener al menos un carácter especial.'
],
isPassphrase : false,
strong : false,
optionalTestsPassed : 1
}
```

Por lo que:

- `errors` es un `array` de `string`s de mensajes de error asociados con las pruebas fallidas.

- `failedTests` enumera qué pruebas han fallado, comenzando desde 0 con la primera prueba requerida

- `passedTests` enumera qué pruebas han tenido éxito, comenzando desde 0 con la primera prueba requerida

- `requiredTestErrors` es una matriz que contiene los mensajes de error de las pruebas requeridas que han fallado.

- `optionalTestErrors` es una matriz que contiene los mensajes de error de las pruebas opcionales que han fallado.

- `isPassphrase` es un `boolean` que indica si la contraseña se consideró o no una frase de contraseña.

- `strong` es un `boolean` que indica si la contraseña del usuario cumplió o no con los requisitos de seguridad.

- `optionalTestsPassed` es un `number` que indica cuántas de las pruebas opcionales se aprobaron.
  Para que la contraseña se considere "segura", debe ser (por defecto) una frase de contraseña,
  o debe pasar una cantidad de pruebas opcionales que sea igual o mayor que `configs.minOptionalTestsToPass`.

### Configuración

El módulo se puede configurar de la siguiente manera:

```javascript
var owasp = require("owasp-password-strength-test");

// Pase un hash de configuraciones al método `config`. Las configuraciones que se muestran aquí son
// las predeterminadas.
owasp.config({
  allowPassphrases: true,
  maxLength: 128,
  minLength: 10,
  minPhraseLength: 20,
  minOptionalTestsToPass: 4,
});
```

Por lo que:

- `allowPassphrases` es un `boolean` que activa y desactiva el mecanismo de "frase de contraseña".

- `false`, el verificador de fortaleza abandonará la noción de "frases de contraseña" y someterá todas las contraseñas a los mismos requisitos de complejidad.

- `maxLength` es una restricción sobre la longitud máxima de una contraseña.

- `minLength` es una restricción sobre la longitud mínima de una contraseña.

- `minPhraseLength` es la longitud mínima que una contraseña debe alcanzar para ser considerada una "frase de contraseña" (y, por lo tanto, exenta de las pruebas de complejidad opcionales de forma predeterminada).

- `minOptionalTestsToPass` es la cantidad mínima de pruebas opcionales que debe pasar una contraseña para que se la considere "segura".
  De manera predeterminada (según las pautas de OWASP), se realizan cuatro pruebas de complejidad opcionales y una contraseña debe pasar al menos tres de ellas para que se la considere "segura".

### Ampliación

Si desea filtrar contraseñas mediante pruebas adicionales a las predeterminadas, puede simplemente insertar nuevas pruebas en las matrices adecuadas dentro del objeto `test` del módulo:

```javascript
var owasp = require("owasp-password-strength-test");

// inserte las pruebas "obligatorias" en el array `tests.required` y las pruebas "opcionales"
// en la matriz `tests.optional`.
owasp.tests.required.push(function (password) {
  if (password === "one two three four five") {
    return "¡Ese es el tipo de cosas que un idiota llevaría en su equipaje!";
  }
});
```

Las funciones de prueba deben parecerse a las siguientes:

```javascript
// aceptar la contraseña como único argumento
function(password) {

// la condición "if" debe evaluarse como `true` si la contraseña es incorrecta
if (thePasswordIsBad) {

// Si falla la contraseña, se debe devolver una cadena. Se insertará
// en una matriz de errores asociados con la contraseña.
return "Este es el mensaje de error asociado con la prueba";
}

// si la contraseña es correcta, no se debe devolver nada
}
```

### Pruebas

Para ejecutar el conjunto de pruebas del módulo, haga `cd` en su directorio y ejecute `npm test`.
Es posible que primero deba ejecutar `npm install` para instalar las dependencias de desarrollo necesarias. (Estas dependencias **no** son necesarias en un entorno de producción y solo facilitan las pruebas unitarias).

### Limitaciones

OWASP Password Strenght Test es un copycat de <a href="https://github.com/nowsecure/owasp-password-strength-test" target="_blank" rel="noreferrer noopener">NOWSECURE</a> y solo tiene fines educativos bajo la licencia MIT.

---

<h3 align="left">Conecta Conmigo</h3>

<p align="left">
<a href="https://www.youtube.com/@gabriellugooo" target="_blank" rel="noreferrer noopener"> <img align="center" src="https://img.icons8.com/?size=50&id=55200&format=png" alt="@gabriellugooo" height="40" width="40" /></a>
<a href="http://www.tiktok.com/@gabriellugooo" target="_blank" rel="noreferrer noopener"> <img align="center" src="https://img.icons8.com/?size=50&id=118638&format=png" alt="@gabriellugooo" height="40" width="40" /></a>
<a href="https://instagram.com/lugooogabriel" target="_blank" rel="noreferrer noopener"> <img align="center" src="https://img.icons8.com/?size=50&id=32309&format=png" alt="lugooogabriel" height="40" width="40" /></a>
<a href="https://twitter.com/gabriellugo__" target="_blank" rel="noreferrer noopener"> <img align="center" src="https://img.icons8.com/?size=50&id=phOKFKYpe00C&format=png" alt="gabriellugo__" height="40" width="40" /></a>
<a href="https://www.linkedin.com/in/hernando-gabriel-lugo" target="_blank" rel="noreferrer noopener"> <img align="center" src="https://img.icons8.com/?size=50&id=8808&format=png" alt="hernando-gabriel-lugo" height="40" width="40" /></a>
<a href="https://github.com/GabrielLugooo" target="_blank" rel="noreferrer noopener"> <img align="center" src="https://img.icons8.com/?size=80&id=AngkmzgE6d3E&format=png" alt="gabriellugooo" height="34" width="34" /></a>
<a href="mailto:lugohernandogabriel@gmail.com"> <img align="center" src="https://img.icons8.com/?size=50&id=38036&format=png" alt="lugohernandogabriel@gmail.com" height="40" width="40" /></a>
<a href="https://linktr.ee/gabriellugooo" target="_blank" rel="noreferrer noopener"> <img align="center" src="https://simpleicons.org/icons/linktree.svg" alt="gabriellugooo" height="40" width="40" /></a>
</p>

<p align="left">
<a href="https://github.com/GabrielLugooo/GabrielLugooo/blob/main/Readme%20Spanish.md" target="_blank" rel="noreferrer noopener"> <img align="center" src="https://img.shields.io/badge/Versión%20Español-000000" alt="Versión Español" /></a>
<a href="https://github.com/GabrielLugooo/GabrielLugooo/blob/main/README.md" target="_blank" rel="noreferrer noopener"> <img align="center" src="https://img.shields.io/badge/Versión%20Inglés-Green" alt="Versión Inglés" /></a>

</p>

<a href="https://linktr.ee/gabriellugooo" target="_blank" rel="noreferrer noopener"> <img align="center" src="https://img.shields.io/badge/Créditos-Gabriel%20Lugo-green" alt="Créditos" /></a>
<img align="center" src="https://komarev.com/ghpvc/?username=GabrielLugoo&label=Vistas%20del%20Perfil&color=green&base=2000" alt="GabrielLugooo" />
<a href="" target="_blank" rel="noreferrer noopener"> <img align="center" src="https://img.shields.io/badge/License-MIT-green" alt="MIT License" /></a>
