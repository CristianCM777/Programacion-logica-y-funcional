# Contexto e Historia de la Programación Funcional

## Orígenes Matemáticos: El Cálculo Lambda (Años 30s)

La programación funcional comienza entre **1932 y 1936**, cuando Alonzo Church desarrolla el **Cálculo Lambda**, un sistema matemático formal para expresar funciones [1], [5]. Church creó una notación elegante (λ) que captura el comportamiento de funciones matemáticas puras. La **tesis de Church–Turing** sostiene que todo lo que una computadora puede calcular puede expresarse en este formalismo; es una tesis ampliamente aceptada, no un teorema demostrado.

## Primer Lenguaje Funcional: LISP (Finales 1950s)

A finales de los **años 1950** (1958–1960), John McCarthy define **LISP**, el primer lenguaje de programación que toma la notación lambda de Church como base [2]. LISP fue revolucionario porque:

- Introdujo garbage collection automático
- Permitió funciones de orden superior y tratar funciones y programas como datos
- Se convirtió en el lenguaje de investigación en IA durante décadas

El LISP original usaba **alcance dinámico**; los closures con alcance léxico se popularizaron después con **Scheme (1975)** [1].

**Dato curioso:** gran parte de la lógica de la serie de videojuegos *Jak and Daxter* (Naughty Dog) se escribió en **GOAL**, un dialecto de Lisp creado por el propio estudio.

## Consolidación: ML y la Era de la Tipificación Estática (1970s–1980s)

En **1973**, en la Universidad de Edimburgo, **Robin Milner** y su equipo crearon **ML** (Meta Language) como lenguaje para describir estrategias de prueba en el demostrador automático **LCF** [1]. ML introdujo:

- Sistemas de tipos estáticos con inferencia Hindley-Milner
- Polimorfismo paramétrico
- Pattern matching sobre tipos de datos algebraicos

Estos avances hicieron la programación funcional **práctica y verificable**, no solo teórica.

**OCaml** (1996) emergió de la familia ML. Heredó de Standard ML el sistema de módulos y functores, y agregó **objetos** y un compilador nativo eficiente [3]. Hoy se usa en investigación y producción; por ejemplo, Meta escribió en OCaml las herramientas de análisis Hack, Flow e Infer.

## Modernización: De OCaml al Ecosistema .NET con F# (2005)

**El problema:** a inicios de los 2000, el ecosistema **.NET de Microsoft** se centraba en lenguajes imperativos y orientados a objetos (C#, VB.NET); no tenía un lenguaje funcional tipado de primera línea.

**La solución:** Don Syme, en Microsoft Research, inició hacia 2002 el proyecto **F#**, llevando los principios de OCaml/ML al CLR (.NET Runtime); la versión 1.0 se publicó en 2005 [3]. F# implementa [3], [4]:

- El sistema de tipos de ML (inferencia Hindley-Milner)
- Inmutabilidad por defecto
- Funciones de orden superior y pattern matching
- **Interoperabilidad completa con C# y librerías .NET**

Esto permitió a desarrolladores de C# acceder a programación funcional sin abandonar el ecosistema Microsoft.

## Relevancia Actual

La programación funcional hoy es relevante porque:

- **Paralelismo:** funciones puras y datos inmutables son más fáciles de paralelizar
- **Confiabilidad:** limitar los efectos secundarios reduce una clase importante de errores
- **Testabilidad:** las funciones puras son determinísticas y fáciles de probar
- **Análisis de datos:** encaja bien con transformaciones de datos en cadena
- **Casos en producción:** WhatsApp (Erlang), Discord (Elixir), Nubank (Clojure) y Jane Street (OCaml) sostienen sistemas críticos con lenguajes funcionales

F# representa la **madurez de este paradigma**, combinando rigor matemático con practicidad industrial en una plataforma ampliamente usada.

---

Referencias: ver la sección *Bibliografía (IEEE)* del [README del equipo](README.md#bibliografía-ieee).
