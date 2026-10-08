# Kata 1 – Cálculo de la edad de una persona

## 1. Objetivo de la entrega

Esta entrega recoge la resolución de la **kata 1**: modelar una persona (nombre y fecha de nacimiento) y calcular su **edad en años** a partir de la fecha actual.

Además del código, la entrega busca practicar el flujo de trabajo completo de un proyecto: control de versiones con Git/GitHub, comprobación de que el proyecto compila desde un clon limpio y documentación del proceso (README y vídeo explicativo).

- Repositorio: <https://github.com/Eldeivi20/kata1>

---

## 2. Dependencias y versión de JDK

| Elemento | Versión / detalle |
|---|---|
| JDK | **23** (`maven.compiler.source` y `maven.compiler.target` = 23) |
| Herramienta de construcción | Maven (`pom.xml` incluido) |
| Codificación | UTF-8 |
| Dependencias externas | **Ninguna** (solo la librería estándar, `java.time.LocalDate`) |
| IDE usado | IntelliJ IDEA |

---

## 3. Cómo compilar y ejecutar

### Con Maven (desde la raíz del proyecto)

```bash
mvn clean compile
```

Las clases compiladas quedan en `target/classes`.

### Con IntelliJ IDEA

1. `File > Open...` y seleccionar la carpeta del proyecto (donde está el `pom.xml`).
2. Esperar a que IntelliJ importe el proyecto Maven.
3. Comprobar que el SDK del proyecto es JDK 23 (`File > Project Structure > Project`).
4. Compilar con `Build > Build Project`.

### Ejecución

El proyecto actual contiene únicamente la clase de dominio `Person` y **no define un método `main`**, por lo que no hay una aplicación ejecutable por sí sola. Para probarla rápidamente se puede usar `jshell` con las clases compiladas:

```bash
jshell --class-path target/classes
```

```java
import software.ulpgc.katas.Person;
import java.time.LocalDate;

var p = new Person("Ana", LocalDate.of(2000, 1, 15));
p.age();
```

---

## 4. Estructura de la entrega y clases principales

```
kata1/
├── .idea/                          # Configuración de IntelliJ
├── .gitignore
├── pom.xml                         # Configuración Maven (JDK 23)
├── README.md
└── src/
    └── main/
        └── java/
            └── software/ulpgc/katas/
                └── Person.java
```

### Clase principal: `Person`

`Person` es un `record` de Java con dos componentes:

- `name` (`String`): nombre de la persona.
- `birthday` (`LocalDate`): fecha de nacimiento.

Elementos destacados:

| Miembro | Descripción |
|---|---|
| `DAYS_PER_YEAR` | Constante con valor `365` usada para convertir días en años. |
| `age()` | Devuelve la edad en años: diferencia entre el día actual (`LocalDate.now()`) y el cumpleaños, ambos en días desde la época (`toEpochDay()`), convertida a años. |
| `toYears(long days)` | Método privado que divide los días entre `DAYS_PER_YEAR` y trunca a `int`. |

> **Nota sobre la precisión:** al dividir entre 365 no se tienen en cuenta los años bisiestos, así que en algunos casos la edad puede adelantarse o retrasarse unos días respecto a la edad real. Una alternativa más exacta sería `ChronoUnit.YEARS.between(birthday, LocalDate.now())` o `Period.between(birthday, LocalDate.now()).getYears()`.

---

## 5. Flujo Git usado

- **Rama principal:** `master`.
- **Commits:** el repositorio tiene actualmente 6 commits en `master`:

  ```bash
  git log --oneline
  ```

 commit 4f9a6b4e48899488507a6a8ded64988ffa2a0d7d (HEAD -> master, origin/master)
Author: Eldeivi20 <davidsarmiensantana@gmail.com>
Date:   Sun Sep 27 20:45:06 2026 +0100

    POM updated

commit 91f1ab29f6565f1fa053eae06d8bf8bf8b64375e
Author: Eldeivi20 <davidsarmiensantana@gmail.com>
Date:   Sun Sep 27 20:41:55 2026 +0100

    Class with birthday and age attributes

commit c07a2f47b0842b1d104ef0b7a3c5b8b57fcedc9a
Author: Eldeivi20 <davidsarmiensantana@gmail.com>
Date:   Sun Sep 27 20:28:47 2026 +0100

    Class Person as record

commit bbc4d9d3c93519ff8055f05e402dba11abe69882
Author: Eldeivi20 <davidsarmiensantana@gmail.com>
Date:   Sun Sep 27 20:27:20 2026 +0100

    Class Person with name Attribute

commit tbcgfsdtr8673ryuyg7i6wge402dba11abe32173
Author: Eldeivi20 <davidsarmiensantana@gmail.com>
Date:   Sun Sep 27 20:20:36 2026 +0100

    Class Person Created

commit fdhi87ty43hbgiudyfh873047vh7dhb8793g0472
Author: Eldeivi20 <davidsarmiensantana@gmail.com>
Date:   Sun Sep 27 20:15:18 2026 +0100

    Project Created

---

## 6. Vídeo explicativo

-[ Enlace:](https://youtu.be/5AudHPksERg)

---

## Autor

**Eldeivi20** – Universidad de Las Palmas de Gran Canaria (ULPGC)
