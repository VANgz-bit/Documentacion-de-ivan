#  El Objeto `Date` en JavaScript (Versión Extendida)

El objeto `Date` es el mecanismo principal en JavaScript para representar **fechas y horas**. Internamente funciona como un número entero que cuenta los **milisegundos transcurridos desde el 1 de enero de 1970 a las 00:00:00 UTC** (lo que se conoce como _Epoch_).  
Este sistema hace que `Date` sea flexible: cualquier fecha y hora puede calcularse como una cantidad positiva o negativa de milisegundos desde ese punto.

Gracias a ello, JavaScript puede:

- Crear instantes de tiempo específicos.
    
- Descomponer fechas en sus partes (año, mes, día, hora, etc.).
    
- Formatear fechas en texto legible.
    
- Realizar operaciones con tiempo (sumar o restar días, horas, etc.).
    

---

## 1. Creación de Fechas

Existen varias formas de construir un objeto `Date`.

### 1.1. Fecha actual

```js
let ahora = new Date();
console.log(ahora);
```

📌 Esto muestra la fecha y hora exactas del momento de ejecución, en el formato completo de la zona horaria local.  
Ejemplo de salida:

```
Wed Oct 01 2025 12:30:15 GMT-0300 (Argentina Standard Time)
```

---

### 1.2. Desde una cadena de texto

```js
let fecha1 = new Date("2025-10-01T10:00:00");
console.log(fecha1);
```

📌 Se crea un objeto `Date` a partir de un **string con formato reconocible** (ISO 8601 es el más confiable).  
Ejemplo de salida:

```
Wed Oct 01 2025 10:00:00 GMT-0300 (Argentina Standard Time)
```

---

### 1.3. Con parámetros separados

```js
let fecha2 = new Date(2025, 9, 1, 10, 0, 0);
console.log(fecha2);
```

📌 Se construye usando:  
`new Date(año, mes, día, hora, minuto, segundo, milisegundo)`

⚠️ Importante: **los meses comienzan en 0** (0 = enero, 9 = octubre).

Ejemplo de salida:

```
Wed Oct 01 2025 10:00:00 GMT-0300 (Argentina Standard Time)
```

---

### 1.4. Con milisegundos desde el Epoch

```js
let fecha3 = new Date(0);
console.log(fecha3);
```

📌 Crea la fecha correspondiente al 1 de enero de 1970 a las 00:00:00 UTC.

Salida:

```
Thu Jan 01 1970 00:00:00 GMT+0000 (Coordinated Universal Time)
```

---

## 2. Métodos de Obtención (Getters)

Los **getters** permiten descomponer una fecha y acceder a sus componentes individuales.

---

### 2.1. `getFullYear()`

Devuelve el **año completo en cuatro dígitos**.

```js
let fecha = new Date("2025-10-01T10:00:00");
console.log(fecha.getFullYear());
```

Salida:

```
2025
```

---

### 2.2. `getMonth()`

Devuelve el número de mes (0 = enero, 11 = diciembre).

```js
console.log(fecha.getMonth());
```

Salida:

```
9   // Octubre
```

---

### 2.3. `getDate()`

Devuelve el **día del mes** (1 a 31).

```js
console.log(fecha.getDate());
```

Salida:

```
1
```

---

### 2.4. `getDay()`

Devuelve el **día de la semana** (0 = domingo, 6 = sábado).

```js
console.log(fecha.getDay());
```

Salida:

```
3   // Miércoles
```

---

### 2.5. `getHours()`, `getMinutes()`, `getSeconds()`, `getMilliseconds()`

Devuelven las partes horarias.

```js
let ahora = new Date("2025-10-01T15:45:30.123");
console.log(ahora.getHours());        // 15
console.log(ahora.getMinutes());      // 45
console.log(ahora.getSeconds());      // 30
console.log(ahora.getMilliseconds()); // 123
```

---

### 2.6. `getTime()`

Devuelve el **número de milisegundos desde el Epoch**.

```js
console.log(fecha.getTime());
```

Salida:

```
1759311600000
```

---

### 2.7. `getTimezoneOffset()`

Devuelve la diferencia (en minutos) entre UTC y la hora local.

```js
console.log(fecha.getTimezoneOffset());
```

Ejemplo:

```
180   // Significa UTC-3 (Argentina)
```

---

### 2.8. Versiones en UTC

Todos los métodos anteriores tienen versiones en UTC, como:  
`getUTCFullYear()`, `getUTCMonth()`, `getUTCDate()`, etc.  
Sirven para obtener la fecha sin aplicar la zona horaria local.

```js
console.log(fecha.getUTCFullYear()); // 2025
```

---

## 3. Métodos de Establecimiento (Setters)

Estos métodos permiten **modificar directamente un objeto `Date`**, alterando su estado interno.

---

### 3.1. `setFullYear(año)`

Cambia el año.

```js
fecha.setFullYear(2030);
console.log(fecha.toString());
```

Salida:

```
Tue Oct 01 2030 10:00:00 GMT-0300 (Argentina Standard Time)
```

---

### 3.2. `setMonth(mes)`

Cambia el mes (0 a 11).

```js
fecha.setMonth(0); // enero
console.log(fecha.toString());
```

Salida:

```
Tue Jan 01 2030 10:00:00 GMT-0300 (Argentina Standard Time)
```

---

### 3.3. `setDate(día)`

Cambia el día del mes.

```js
fecha.setDate(15);
console.log(fecha.toString());
```

Salida:

```
Tue Jan 15 2030 10:00:00 GMT-0300 (Argentina Standard Time)
```

---

### 3.4. `setHours()`, `setMinutes()`, `setSeconds()`, `setMilliseconds()`

Modifican las partes horarias.

```js
fecha.setHours(12);
fecha.setMinutes(30);
console.log(fecha.toString());
```

Salida:

```
Tue Jan 15 2030 12:30:00 GMT-0300 (Argentina Standard Time)
```

---

### 3.5. `setTime(ms)`

Define la fecha exacta a partir de milisegundos desde el Epoch.

```js
fecha.setTime(0);
console.log(fecha.toString());
```

Salida:

```
Thu Jan 01 1970 00:00:00 GMT+0000 (Coordinated Universal Time)
```

---

## 4. Métodos de Conversión a Texto

Permiten convertir una fecha en **cadena legible**.

---

### 4.1. `toString()`

Representación completa local.

```js
console.log(new Date().toString());
```

Salida:

```
Wed Oct 01 2025 12:45:00 GMT-0300 (Argentina Standard Time)
```

---

### 4.2. `toDateString()`

Solo la parte de la fecha.

```js
console.log(new Date().toDateString());
```

Salida:

```
Wed Oct 01 2025
```

---

### 4.3. `toTimeString()`

Solo la parte de la hora.

```js
console.log(new Date().toTimeString());
```

Salida:

```
12:45:00 GMT-0300 (Argentina Standard Time)
```

---

### 4.4. `toUTCString()`

Fecha en formato UTC.

```js
console.log(new Date().toUTCString());
```

Salida:

```
Wed, 01 Oct 2025 15:45:00 GMT
```

---

### 4.5. `toISOString()`

Formato ISO 8601 (el más usado en APIs).

```js
console.log(new Date().toISOString());
```

Salida:

```
2025-10-01T15:45:00.000Z
```

---

### 4.6. `toLocaleString()`, `toLocaleDateString()`, `toLocaleTimeString()`

Adaptan la salida según la configuración regional.

```js
let fecha = new Date();
console.log(fecha.toLocaleString("es-AR"));  
console.log(fecha.toLocaleDateString("es-AR"));  
console.log(fecha.toLocaleTimeString("es-AR"));  
```

Salida:

```
1/10/2025 12:45:00
1/10/2025
12:45:00
```

---

## 5. Métodos Estáticos

---

### 5.1. `Date.now()`

Devuelve el timestamp actual en milisegundos.

```js
console.log(Date.now());
```

Salida:

```
1759311900000
```

---

### 5.2. `Date.parse(cadena)`

Convierte una cadena en milisegundos desde Epoch.

```js
console.log(Date.parse("2025-10-01T10:00:00"));
```

Salida:

```
1759311600000
```

---

### 5.3. `Date.UTC(año, mes, día, ...)`

Devuelve milisegundos desde Epoch en UTC.

```js
console.log(Date.UTC(2025, 9, 1, 10, 0, 0));
```

Salida:

```
1759312800000
```

---

📌 **En resumen:**

- Los **getters** extraen partes de la fecha.
    
- Los **setters** modifican directamente el objeto.
    
- Los métodos de **conversión** transforman la fecha en texto (normal, local, ISO, etc.).
    
- Los métodos **estáticos** permiten obtener timestamps o construir fechas en UTC.
    

---
