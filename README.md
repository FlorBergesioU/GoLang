# GoLang

## Notas
- Se puede correr un desarrollo en go con go run main.go
- Se puede buildear un desarrollo en go con go build main.go
- El ejecutable de go tiene todo lo necesario para poder ejecutarse desde cualquier sistema operativo
- Las funciones en go deben abrir llaves en la misma linea donde se define el nombre

## Variables
Existen 3 tipos de variables:
- Numerics: Enteras (int, int8, etc), enteras sin signo (uint, uint8, etc), punto flotante (float32, float64, etc). Se inicializan con 0
- Strings: (string). Se inicializan con cadena vacía
- Booleans: (bool). Se inicializan con false
Para definir una variable se utilizan las sintaxis: 
- var var1, var2, var3 int
- var nombre_variable tipo_variable = valor_variable
- nombre_variable := valor variable
- var1, var2, var3 := 5
- var1, var2, var3 := 1, 2, "Texto"
Parseo:
- Los numeros se pueden parsear a numeros enteros de la siguiente forma: int(variable_valor_int64)
- Los string necesitan el uso de paquetes: fmt.Sprintf("%d", variable_valor_int64) o strconv.Itoa(int(variable_valor_int64))
- Los valores nulos son "nil"

## Scope
El scope de las variables, métodos y funciones se determina de la siguiente manera:
- Si el nombre comienza con una letra minuscula, es privado
- Si el nombre comienza con una letra mayuscula, se exporta a otros scope (paquetes, desarrollos, etc)
- Si una variable se define fuera de las funciones, puede ser utilizada por todas las funciones del paquete
- Si una variable se define dentro de esa funcion, su scope se limita a esa funcion

## Paquete main
- El archivo principal de un desarrollo en go es main.go
- Debe tener la definicion de package main
- La funcion main es la entrada al programa

## Sentencia if
- No hace falta usar los paréntesis a menos que sea necesario agrupar condiciones
- Se pueden asignar variables dentro de la sentencia if y estas variables serán accesibles en el cuerpo del if y else: if estado=false; estado == true {...}

## Sentencia switch
- No hace falta usar los paréntesis a menos que sea necesario agrupar condiciones
- Se pueden asignar variables dentro de la sentencia if y estas variables serán accesibles en el cuerpo del switch: switch numero := 5; numero { case 1: ... }
- No hace falta utilizar el break

## Sentencia for
- No hace falta usar los paréntesis a menos que sea necesario agrupar condiciones
- Reemplaza a todas las otras sentencias de ciclos disponibles en otro lenguajes
- No hace falta inicializar la variable i en el ciclo, se puede inicializar afuera
- No hace falta agregar un incremento a i en el ciclo, se puede agregar en el cuerpo del ciclo
- No hace falta agregar una condición de checkeo en el ciclo, se puede dejar vacío y salir del mismo con un break
- Por ejemplo, puede haber un for {...} que se ejecutará indefinidamente, hasta que algo dentro del cuerpo llege a una sentencia break
- Se puede utilizar la sentencia continue para mandar la ejecución al inicio del ciclo for en una nueva iteracion

## Sentencia goto
- Se puede definir un inicio de bloque utilizando un nombre en mayusculas y dos puntos. Ejemplo -> RUTINA:
- Se puede redireccionar el flujo de ejecución a este bloque utilizando la sentencia goto RUTINA

## Funciones
- Estructura: func nombre_funcion(nombre_parametro tipo_de_dato, nombre_parametro tipo_de_dato) (tipo_de_dato_return, tipo_de_dato_return) {... return valor, valor}
- No hace falta usar los parentesis en el tipo de dato de retorno si solo es 1
- Podemos recuperar los datos de return de esta forma: var1, var2 := nombre_funcion(parametros)
- Se puede definir un nombre de variable para un valor de retorno, en ese caso al escribir unicamente return se retornará el valor actual de dicha variable
- No existe la sobrecarga de funciones en Go
- Podemos definir que una funcion puede recibir un numero indefinido de parametros, usando la funcion range y el "_" para el valor de retorno que no nos interesa: suma(numero ...int) {
    for _, num := range numero{...}
}

## Funciones anónimas
- Se pueden definir variables del tipo func que contengan funciones anónimas, las cuales pueden cambiar en tiempo de ejecución
- Se debe respetar la definicion inicial de parametros y valores de return

### Closures
- Pueden acceder a variables creadas fuera de la función (en la función "original")
- Si se ejecuta varias veces la función, el código dentro de la funcion original pero fuera del closure solo se ejecutará la primera vez

## Vectores
- Los vectores no pueden variar sus dimensiones en tiempo real

### Slices
- Vectores que pueden variar sus dimensiones en tiempo real
- Se definen al no indicar la longitud en los corchetes. Ej: slice:= []int
- También se pueden crear utilizando la función make, la cual acepta los parámetros de longitud inicial y maximo de longitud reservada en memorita. Ej: slice := make([]int,5,20)
- El largo de un slice se puede obtener con len(nombreSlice), mientras que la capacidad máxima reservada en memoria se puede obtener con cap(nombreSlice)
- Se pueden agregar elementos mas alla de la capacidad definida, pero deberá hacerse con append(nombreSlice, elemento). En este caso si no se define un cap, se definirá automaticamente segun una potencia de 2

### Maps
- Los mapas permiten crear pares de clave y valor asociado.
- Pueden crearse con la función make, indicando el tipo de la clave entre corchetes y el tipo del valor asociado. Ej: make(map[string]int)
- Los elementos del maps se ordenan alfabeticamente por la clave
- Se puede añadir un elemento con una asignación, y eliminar un elemento con la función delete
- Si queremos recorrer un map en un orden diferente al alfabetico, podemos utilizar un for con 2 variables y range

## OOP - Estructuras
- Go implementa la OOP mediante estructuras
- No puede poseer métodos, solo propiedades

### Interfaces
- Permite nombrar métodos que serán implementados por structs
- No es necesario indicar explicitamente que interfaz utiliza un struct, Go lo detecta automaticamente

## Manejo de archivos
Refer to /file_management/main.go

## Paralelism

### Rutinas go
- Para que una funcion se ejecute de manera asincrona se le debe anteponer la instrucción "go" al llamado a la misma
- Ejecutar una rutina con go no verifica que la función se haya terminado de ejecutar antes de terminar el programa

### Channels
- Nos permiten enviar información de una go routine hacia otra funcion u otra go routine, para que cada instrucción paralela pueda comunicarse y para poder tomar el control
- Es un espacio de memoria, de dialogo. Cuando se aloje en este espacio un valor, la rutina que está pidiendo un valor a cambio, va a actuar en consecuencia. Mientras que no se reciba un valor, se detiene la ejecucion del resto del programa
- Para asignar valores a un channel: nombre_channel <- valor
- Para esperar un valor de un channel: nombre_variable := <- nombre_channel

## Excepciones
- Defer: Instrucción que se ejecuta si o si cuando una funcion termina, ya sea por un return, por un error o por llegar al fin de la misma
- Panic: Instrucción para que el sistema aborte la ejecución
- Recover: Permite recuperar la ejecución del programa tras un Panic. Se ejecuta cuando detecta un Panic. Se usan en conjunto con los Defer

## Web server
Refer to /web_server.main.go

## Middlewares
- Son interceptores que permiten ejecutar instrucciones comunes a varias funciones que reciben y devuelven los mismos tipos de variables

## Testing
- Para crear una prueba en Go, se debe crear un archivo cuyo nombre termine en "_test.go"
- Para ejecutar las pruebas usamos el comando "go test"
- go test main.go main_test.go

## Librerias utiles
- fmt: permite mostrar textos por pantalla, grabar texto en archivos
- os: permite manejar cuestiones del sistema operativo
- bufio: permite aceptar entradas por teclado
- time: permite manejar fechas y tipos de datos fecha y hora - es un paquete de go
- io/ioutil: permite el manejo de archivos
- log: permite grabar en el log
- strings: permite el manejo de strings
- net/http: permite el manejo de webserver

### Librerias propias
- En la carpeta del proyecto podemos crear una nueva carpeta con el nombre del paquete a crear, asi como el nombre del archivo principal.
- En el archivo principal del proyecto definimos el nombre del paquete
- Doc para modulos: https://go.dev/doc/tutorial/create-module

### Paquete fmt - verbos
- %d - numérico, base 10
- %s - string
- %t - boolean
- %v - valor variable

### Paquete log - funciones
- Fatalf - Función que muestra un mensaje personalizado de error, anexa información de fecha y hora del error, además de ejecutar una función os.Exit(1)