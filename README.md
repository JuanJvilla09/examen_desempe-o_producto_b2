# examen_desempe-o_producto_b2


## Descripción

Este proyecto está desarrollado con **Spring Boot** y utiliza **JPA/Hibernate** para la persistencia de datos en una base relacional MySQL. Con gestor de dependecias de Gradle

El modelo incluye las entidades principales:

- **Usuario**: Representa a los usuarios del sistema.
- **Docente**: Asociado a un usuario, representa a un docente.
- **Curso**: Cursos impartidos por un docente.

Relaciones principales:

- Un usuario puede estar asociado a un docente (1:1).
- Un docente puede impartir muchos cursos (1:N).

---

## Errores corregidos

### Usuario.java

| Error                                | Descripción                                            | Solución                                    |
|-------------------------------------|--------------------------------------------------------|---------------------------------------------|
| `@Entit` en vez de `@Entity`        | Error tipográfico que bloquea el reconocimiento JPA. | Corregido a `@Entity`.                      |
| `@GeneratedValue(strategy = GenerationType.)` incompleto | Falta la estrategia para generación automática del ID. | Corregido a `GenerationType.IDENTITY`.     |
| `@Colun` en lugar de `@Column`      | Error tipográfico en anotaciones de columnas.          | Corregido a `@Column`.                      |
| Falta anotaciones en contraseña y teléfono | Sin restricciones ni mapeo adecuado.                   | Añadidas anotaciones `@Column` con atributos.|

### Docente.java

| Error                 | Descripción                              | Solución                  |
|-----------------------|------------------------------------------|---------------------------|
| `@Entit` incorrecto    | Error tipográfico en anotación JPA.      | Corregido a `@Entity`.    |
| Falta `@Id` en `id`   | Clave primaria no definida.               | Añadido `@Id`.            |
| Falta `@Column` en especialidad | Buenas prácticas para definir columnas. | Añadido `@Column(nullable = false, length = 50)` |

### Curso.java

| Error                             | Descripción                                | Solución                                      |
|----------------------------------|--------------------------------------------|-----------------------------------------------|
| Falta `@Entity`                  | Clase no reconocida como entidad JPA.       | Añadido `@Entity`.                            |
| `@I` en lugar de `@Id`           | Error tipográfico clave primaria.            | Corregido a `@Id`.                           |
| `@Ge(strategy = IDENTITY)` mal escrita | Anotación incorrecta.                         | Corregido a `@GeneratedValue(strategy = GenerationType.IDENTITY)`. |
| Falta punto y coma y modificadores| Error de sintaxis en atributos.               | Corregido agregando `private` y `;`.          |
| `@JoinColumn` con `;`             | Sintaxis incorrecta tras anotación.            | Eliminado `;` tras la anotación.               |

---

## Guía para conexión a la base de datos

1. **Dependencias Gradle

```
plugins {
	id 'java'
	id 'org.springframework.boot' version '3.5.4'
	id 'io.spring.dependency-management' version '1.1.7'
}

group = 'com.example'
version = '0.0.1-SNAPSHOT'

java {
	toolchain {
		languageVersion = JavaLanguageVersion.of(17)
	}
}

repositories {
	mavenCentral()
}

dependencies {
	implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
	implementation 'org.springframework.boot:spring-boot-starter-web'
	developmentOnly 'org.springframework.boot:spring-boot-devtools'
	runtimeOnly 'com.h2database:h2'
	runtimeOnly 'com.mysql:mysql-connector-j'
	testImplementation 'org.springframework.boot:spring-boot-starter-test'
	testRuntimeOnly 'org.junit.platform:junit-platform-launcher'
}

tasks.named('test') {
	useJUnitPlatform()
}

```
# **Creacion de ENUM TipoUsuario**
```
package com.example.Examen1Back2.ayudas;

public enum TipoUsuario {
    Estudiante,
    Empresario,
    Empleado,
    Becado,
    Egresado
```





