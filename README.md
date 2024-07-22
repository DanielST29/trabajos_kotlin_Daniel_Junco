By Daniel Junco

CODIGO PARA IMPRIMIR HELLO Y MI NOMBRE DANIEL JUNCO:
package co.edu.sena.myappjetpackcompose
import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.activity.enableEdgeToEdge
import androidx.compose.foundation.layout.fillMaxSize
import androidx.compose.foundation.layout.padding
import androidx.compose.material3.Scaffold
import androidx.compose.material3.Text
import androidx.compose.runtime.Composable
import androidx.compose.ui.Modifier
import androidx.compose.ui.tooling.preview.Preview
import co.edu.sena.myappjetpackcompose.ui.theme.MyAppJetpackComposeTheme
class MainActivity : ComponentActivity() {
override fun onCreate(savedInstanceState: Bundle?) {
super.onCreate(savedInstanceState)
enableEdgeToEdge()
setContent {
MyAppJetpackComposeTheme {
Scaffold(modifier = Modifier.fillMaxSize()) { innerPadding ->
Greeting(
name = "Daniel Junco",
modifier = Modifier.padding(innerPadding)
)
}
}
}
}
}
@Composable
fun Greeting(name: String, modifier: Modifier = Modifier) {
Text(
text = "Hello $name!",
modifier = modifier
)
}
@Preview(showBackground = true)
@Composable
fun GreetingPreview() {
MyAppJetpackComposeTheme {
Greeting("Android")
}
}

CONSULTAS:

-DEFINICION DE VARIABLES:

RTA: En Android Studio, cuando trabajamos con Kotlin se definen de
forma diferente las variables dependiendo del contexto.

*Variables de Clase (Propiedades):
Se definen dentro de la clase pero fuera de cualquier función.
Pueden ser val (inmutables) o var (mutables).

Ejemplo de variables de Clase:

class MainActivity : AppCompatActivity() {
// Variable inmutable (propiedad)
val appName: String = "Mi Aplicación"
// Variable mutable (propiedad)
var clickCount: Int = 0
override fun onCreate(savedInstanceState: Bundle?) {
super.onCreate(savedInstanceState)
setContentView(R.layout.activity_main)
// Inicialización de una variable local
val welcomeMessage = "Bienvenido a $appName"
// Uso de la variable mutable
clickCount += 1
// Mostrar el mensaje de bienvenida
Toast.makeText(this, welcomeMessage, Toast.LENGTH_SHORT).show()
}
}

*Variables Locales:
Se definen dentro de funciones o bloques de código.
Solo son accesibles dentro de ese ámbito específico.

Ejemplo de variables locales:
override fun onCreate(savedInstanceState: Bundle?) {
super.onCreate(savedInstanceState)
setContentView(R.layout.activity_main)
// Variable local
val welcomeMessage: String = "Bienvenido a ${appName}"
// Modificación de una variable mutable de clase
clickCount += 1
// Mostrar un mensaje
Toast.makeText(this, welcomeMessage, Toast.LENGTH_SHORT).show()
}

Tipos de Variables:

Variables Inmutables ('val'):
val mensaje: String = "Hola, Mundo"
// mensaje = "Adiós, Mundo" // Esto causaría un error de compilación

Variables Mutables ('var'):
var contador: Int = 0
contador += 1 // Esto es válido

Variables Nullables (Que pueden contener un valor null):
var nombre: String? = null // 'nombre' puede ser null o contener un String.
nombre = "María"           // Asignación de un valor no nulo.

Inicialización Tardía (lateinit)
Para variables que se inicializarán más tarde, se puede usar
lateinit (solo aplicable a var):
lateinit var nombre: String
fun inicializarNombre() {
nombre = "Pedro"
}


-MANEJO DE NULOS:

RTA:El manejo de nulos en Kotlin es uno de sus aspectos más potentes
y seguros en comparación con otros lenguajes. Kotlin tiene un
enfoque muy estricto para evitar los errores de null
(NullPointerExceptions o NPEs), que son una de las
causas más comunes de fallos en las aplicaciones.

-Tipos Nullable y No-Nullable:
En Kotlin, los tipos son no-null por defecto.
Esto significa que una variable de tipo no-null
no puede contener un valor null.

var nombre: String = "Juan" // nombre no puede ser null
// nombre = null // Esto causaría un error de compilación

Para permitir que una variable contenga un valor null,
se utiliza el operador ? después del tipo:
var nombre: String? = "Juan" // nombre puede ser null
nombre = null // Esto es válido

Operadores de Seguridad Nula
Kotlin proporciona varios operadores para
manejar la seguridad nula de manera segura y conveniente.

Operador de Llamada Segura (?.)
Permite ejecutar una llamada a un método o acceso a una propiedad
solo si la variable no es null. Si la variable es null,
la expresión devuelve null:
val longitud: Int? = nombre?.length

Operador Elvis (?:)
Proporciona un valor predeterminado si la variable es null:
val longitud: Int = nombre?.length ?: 0

Operador de Aserción No-Nula (!!)
Convierte cualquier valor en un tipo no-null y
lanza una excepción NullPointerException si el valor es null:
val longitud: Int = nombre!!.length

Uso de Nullability en Funciones
Funciones con Parámetros Nullable
Podemos definir funciones que acepten parámetros nullable:
fun saludar(nombre: String?) {
if (nombre != null) {
println("Hola, $nombre")
} else {
println("Hola, Junco")
}
}

Valores de Retorno Nullable
Podemos definir funciones que retornen valores nullable:
fun obtenerNombre(): String? {
return null // O retorna un String válido
}

Tipos de Colecciones Nullables: Las colecciones en Kotlin también
pueden manejar nulos. Podemos tener colecciones que permiten null
como elementos:
val lista: List<String?> = listOf("A", null, "C")

Funciones de Extensión Null-Safe: Podemos definir funciones
de extensión que operen de manera segura en tipos nullable.
fun String?.imprimirLongitud() {
if (this != null) {
println("Longitud: $length")
} else {
println("La cadena es null")
}
}
val cadena: String? = null
cadena.imprimirLongitud() // Imprime: La cadena es null

El manejo de nulos en Kotlin está diseñado para reducir
significativamente la probabilidad de errores relacionados con
nulos en tiempo de ejecución, proporcionando un enfoque más seguro
y robusto en comparación con muchos otros lenguajes de programación.



-OPCIONALES:

RTA: En Kotlin, los "opcionales" (optional values) se manejan
mediante el concepto de "null safety" o seguridad contra valores
nulos. Este concepto está diseñado para evitar el problema común de
los errores de referencia nula (NullPointerException) que ocurren
en muchos lenguajes de programación, como Java.

Tipos Nullable y No-Nullable:

Tipos No-Nullable
En Kotlin, por defecto, las variables no pueden contener valores
nulos. Por ejemplo:
val a: String = "Hello"  // 'a' no puede ser null
Intentar asignar null a a resultará en un error de compilación.

Tipos Nullable
Para permitir que una variable pueda ser null,
se utiliza el operador ? después del tipo de la variable:
val b: String? = "Hola"  // 'b' puede ser null
val c: String? = null     // 'c' es null

Operadores y Constructos para Manejar Tipos Nullable
Kotlin proporciona varios mecanismos para trabajar con tipos nullable de
manera segura.

Operador de Llamada Segura (?.)
Permite acceder a propiedades y métodos de un objeto nullable de manera segura.
Si el objeto es null, la expresión completa se evalúa como null:
val length: Int? = b?.length  // Si 'b' es null, 'length' será null

Operador Elvis (?:)
Proporciona un valor por defecto en caso de que la expresión de la izquierda sea null:
val length: Int = b?.length ?: 0  // Si 'b' es null, 'length' será 0

Operador de Afirmación No Nula (!!)
Convierte cualquier valor nullable en un tipo no-nullable y arroja una excepción si el valor es null:
val length: Int = b!!.length  // Arrojará una excepción si 'b' es null

Smart Casts
Kotlin utiliza la verificación de tipos inteligente para convertir automáticamente un tipo nullable a
su tipo no-nullable dentro de una estructura de control:
if (b != null) {
println(b.length)  // 'b' es automáticamente casteado a 'String' no-nullable
}

Funciones de Alcance (let, apply, run, also, with)
Permiten ejecutar bloques de código en el contexto de un objeto:
b?.let {
println(it.length)
}

EJEMPLO COMPLETO:
fun main() {
val name: String? = "Kotlin"
// Uso de llamada segura
val length1: Int? = name?.length
println("Length using safe call: $length1")
// Uso de operador Elvis
val length2: Int = name?.length ?: 0
println("Length using Elvis operator: $length2")
// Uso de operador de afirmación no nula
try {
val length3: Int = name!!.length
println("Length using non-null assertion: $length3")
} catch (e: Exception) {
println("Exception using non-null assertion: ${e.message}")
}
// Uso de función de alcance 'let'
name?.let {
println("Length using let: ${it.length}")
}
// Uso de smart cast
if (name != null) {
println("Length using smart cast: ${name.length}")
}
}

Resumen:
Kotlin proporciona un enfoque robusto y seguro para manejar valores
opcionales mediante su sistema de tipos nullable y una serie de operadores
y constructos diseñados para trabajar con ellos de manera segura y eficiente.



-COMENTARIOS:

RTA: los comentarios se utilizan para documentar y explicar el código,
al igual que en muchos otros lenguajes de programación.
Hay tres tipos principales de comentarios en Kotlin: comentarios de línea,
comentarios de bloque y comentarios de documentación. A continuación, se
describen cada uno de estos tipos con ejemplos.

Comentarios de Línea:
Los comentarios de línea comienzan con // y se extienden hasta el final de la
línea. Se utilizan para agregar notas breves o explicaciones dentro del código.
Ejemplo:
fun main() {
val greeting = "Hello, World!"  // Esto es un comentario de línea
println(greeting)
}

Comentarios de Bloque:
Los comentarios de bloque comienzan con /* y terminan con */.
Pueden abarcar múltiples líneas y se utilizan para comentarios más
largos o para deshabilitar bloques de código.
Ejemplo:
fun main() {
/* Este es un comentario de bloque
que abarca múltiples líneas.
Se utiliza para explicar secciones más grandes de código. */
val greeting = "Hello, Daniel Junco!"
println(greeting)
}

Comentarios de Documentación:
Los comentarios de documentación en Kotlin comienzan con /** y terminan con */.
Se utilizan para documentar clases, funciones y propiedades.
Pueden incluir etiquetas especiales como @param, @return, y @throws para
describir los parámetros, el valor de retorno y las excepciones de una función,
respectivamente. Estos comentarios se procesan con herramientas de documentación
como Dokka para generar documentación en HTML o en otros formatos.
Ejemplo:
/**
* Esta función suma dos números.
*
* @param a El primer número.
* @param b El segundo número.
* @return La suma de 'a' y 'b'.
  */
  fun sumar(a: Int, b: Int): Int {
  return a + b
  }

Conclusion:
Los comentarios son esenciales para la documentacion y explicacion de codigo.
Dependiendo del contexto podemos usar uno u otro tipo de comentario  y
el uso de estos puede mejorar significativamente la legibilidad y
mantenibilidad del código.

