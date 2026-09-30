# Equipo 2 — Haskell
## Exposición: Introducción a lenguajes funcionales · Unidad 1

## Integrantes y roles

| Rol | Estudiante | Responsabilidad |
|:-:|:--|:--|
| 1 | BARBOZA CARBALLO, DIEGO ANTONIO | Contexto e historia |
| 2 | BOJORQUEZ VALDEZ, VICTOR MANUEL | Modelo de cómputo y sintaxis |
| 3 | CAMACHO OTAÑEZ, JUAN PABLO | Sistema de tipos / runtime |
| 4 | CAMARILLO MOLINA, CRISTIAN | Demo en vivo + caso real |

## Datos del lenguaje

- **Año / origen:** 1990 (comité Haskell)
- **Creador(es):** _Comité Haskell, entre ellos Simon Peyton Jones, Philip Wadler, Paul Hudak y John Hughes_
- **Modelo de evaluación:** perezoso (*lazy*) por defecto
- **Sistema de tipos:** estático, inferencia Hindley-Milner, clases de tipos, `Maybe`/`Either`
- **REPL / herramienta:** `ghci` (GHC)
- **Caso real verificado (obligatorio en pantalla):** Standard Chartered — motor de valuación de derivados en Haskell. _(fuente IEEE abajo)_

## Guion (12–15 min)

1. **Contexto (2 min)** — por qué un comité crea un lenguaje "puro y perezoso".
2. **Modelo de cómputo (3 min)** — expresiones, pureza, evaluación perezosa (listas infinitas).
3. **Tipos / runtime (3 min)** — qué atrapa el compilador antes de correr; `Maybe`/`Either` frente a `null` y excepciones.
4. **Demo en vivo (4 min)** — `ghci` + "Hola Paradigma" (1..10) + 2.º ejemplo idiomático (`take 10 [1..]` o `foldr`).
5. **Caso real + cierre (2 min)** — Standard Chartered con referencia IEEE; conexión con OCaml, Elm y Gleam.

## Contexto
- A finales de los años 1980 existían muchos lenguajes funcionales puros y no estrictos, pero no había un estándar común.
- En 1987 se decidió crear un comité para unificar ideas y definir un lenguaje abierto.
- Haskell 1.0 se publicó en 1990.
- El lenguaje recibió su nombre por el lógico Haskell Curry.
- Su propuesta principal: programación funcional pura, tipos estáticos y evaluación perezosa por defecto.

## Modelo de computo
### Expresiones 
Ejecutar es reducir.
Un programa no es una secuencia de instrucciones de memoria, sino una expresión reescrita paso a paso hasta su forma irreducible.


### Pureza
Transparencia referencial. 
Una expresión siempre da el mismo valor sin producir efectos secundarios ocultos en la memoria.


### Evaluacion perezosa
Listas infinitas. 
Se calcula solo lo estrictamente necesario (call-by-need), lo que permite trabajar con estructuras de datos infinitas con eficiencia de espacio. 


## Sintaxis
### Patrones 
Distinguir por la forma del dato; varias ecuaciones para una función.


### Guardas
Distinguir por condiciones booleanas aplicadas cuando la forma no es suficiente.


### Where
Nombrar expresiones repetidas para calcularlas una vez y usar el nombre.

### Ejemplo de código
```
-- Patrones: una ecuación por cada forma del dato
longitud :: [a] -> Int
longitud []     = 0
longitud (_:xs) = 1 + longitud xs

-- Guardas: condiciones cuando la forma no basta
clasifica :: Int -> String
clasifica n
  | n < 0     = "negativo"
  | n == 0    = "cero"
  | otherwise = "positivo"

-- where: nombrar una subexpresión y calcularla una vez
imc :: Double -> Double -> String
imc peso altura
  | v < 18.5  = "bajo"
  | v < 25    = "normal"
  | otherwise = "alto"
  where v = peso / altura ^ 2

-- Maybe en lugar de null: división segura
divSegura :: Int -> Int -> Maybe Int
divSegura _ 0 = Nothing
divSegura a b = Just (a `div` b)

main :: IO ()
main = do
  print (longitud "Haskell")            -- 7
  putStrLn (clasifica (-3))             -- negativo
  putStrLn (imc 70 1.75)                -- normal
  print (take 10 [1 ..])                -- lista infinita, evaluación perezosa
  print (divSegura 10 2, divSegura 1 0) -- (Just 5,Nothing)
```

## Sistema de tipos
Un sistema de tipos (type system) es un conjunto de reglas que definen cómo se clasifican y utilizan los valores y expresiones dentro de un lenguaje de programación.
Su propósito principal es restringir las operaciones válidas entre diferentes tipos de datos (como enteros, coma flotante, cadenas o estructuras más complejas) para prevenir errores durante la ejecución de un programa.
Haskell posee un sistema de tipos estáticos y fuertemente tipado lo que quiere decir que:
-  Estático: Los tipos se conocen antes de la ejecución del programa.
-  Tipado fuerte: No permite operaciones entre tipos diferentes de forma arbitraria.
### Características clave en Haskell
- **Inferencia Hindley-Milner:** El compilador deduce automáticamente el tipo exacto de las expresiones sin necesidad de escribir tipos explícitamente. Por ejemplo, deduce longitud :: [a] -> Int de forma automática.
  
- **Clases de Tipos (Typeclasses):** Proporcionan polimorfismo ad-hoc controlado (Eq, Ord, Num, Show), permitiendo definir comportamientos comunes con restricciones de tipo.
  
- **Maybe / Either frente a null y Excepciones:** Manejo de ausencias sin null: En lugar de punteros nulos, se utiliza Maybe a (Just x | Nothing), obligando a manejar ambos casos explícitamente durante la compilación. Control de errores explícito: En lugar de lanzar excepciones no controladas en ejecución, se utiliza Either e a (Left error | Right exito).
  
- **Detección Previa a la Ejecución (Evidencia de Compilación):** Si intentamos compilar un error de tipos como main = putStrLn (1 + "a"), el compilador GHC bloquea la ejecución emitiendo la siguiente evidencia formal:

```
error: [GHC-39999]
    • No instance for ‘Num String’ arising from the literal ‘1’
    • In the first argument of ‘(+)’, namely ‘1’
    • In the first argument of ‘putStrLn’, namely ‘(1 + "a")’
    • In the expression: putStrLn (1 + "a")
```

## Comandos exactos del demo

```bash
# Instalación
ghcup install ghc      # https://www.haskell.org/ghcup/

# Hola Paradigma (imprimir 1..10)
ghci
ghci> mapM_ print [1..10]

# Segundo ejemplo idiomático
ghci> take 10 [1..]              -- lista infinita, evaluación perezosa
```

Salida esperada:

```
1
2
3
4
5
6
7
8
9
10
[1,2,3,4,5,6,7,8,9,10]
```

## Grabación de respaldo (asciinema cloud)

- URL: _https://asciinema.org/a/fl0rxxHtJGfDaN7H_
- Cómo: `asciinema rec demo.cast` → `asciinema upload demo.cast`

## Diapositivas

[Presentación Haskell.pdf](https://github.com/user-attachments/files/32539392/Presentacion.Haskell.pdf)


## Bibliografía (IEEE)

1. _[1]P. Hudak, J. Hughes, S. Peyton Jones, y P. Wadler, "A History of Haskell: Being Lazy with Class," en Proceedings of the Third ACM SIGPLAN Conference on History of Programming Languages ​​(HOPL III) , San Diego, CA, USA, 2007, pp. 12-1–12-55. doi: 10.1145/1238844.1238856._
2. _[2]Equipo de GHCup, "GHCup: The Haskell Toolchain Installer", haskell.org, 2026. [En línea]. Disponible: https://www.haskell.org/ghcup/_
3. _[3]G. Dreimanis, "Haskell in Production: Standard Chartered", Serokell, mayo de 2023. [En línea]. Disponible: https://serokell.io/blog/haskell-in-production-standard-chartered_
4. _[4]Peña Marí, R. (1995). La programación funcional en Haskell (Informe No. DIA-95/2). Universidad Complutense de Madrid, Departamento de Informática y Automática._
5. _[5]I. Isaac, “Qué es un type system o sistema de tipos,” Profesional Review, 27 jul. 2025. [En línea]. Disponible en: https://www.profesionalreview.com/2025/07/27/que-es-un-type-system-o-sistema-de-tipos_
6. _[6] L. Augustsson, "Haskell in the Large: Functional Programming at Standard Chartered," Commercial Users of Functional Programming (CUFP / ACM SIGPLAN), 2011._

---

Rúbrica, medio de presentación y reglas: [`../TEMAS-INTRO-LENGUAJES-FUNCIONALES-40.md`](../TEMAS-INTRO-LENGUAJES-FUNCIONALES-40.md)
