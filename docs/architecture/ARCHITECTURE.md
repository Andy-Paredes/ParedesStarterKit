# Arquitectura de Paredes StarterKit

**Versión del documento:** 1.0  
**Estado:** Borrador  
**Sprint:** 0

## 1. Propósito

Este documento define la arquitectura inicial de Paredes StarterKit.

Paredes StarterKit será una base reutilizable para crear aplicaciones empresariales sin repetir funcionalidades comunes como autenticación, usuarios, roles, validaciones, manejo de errores y configuración.

## 2. Objetivos arquitectónicos

La arquitectura debe permitir:

- Separar claramente las responsabilidades.
- Facilitar las pruebas.
- Evitar dependencias innecesarias.
- Reutilizar funcionalidades comunes.
- Cambiar detalles técnicos sin afectar la lógica principal.
- Mantener el proyecto comprensible para nuevos desarrolladores.
- Permitir el crecimiento gradual del producto.

## 3. Principio principal

Las reglas del negocio no deben depender directamente de:

- La interfaz web.
- La base de datos.
- Entity Framework Core.
- Servicios externos.
- Proveedores de correo.
- Sistemas de archivos.

Estas herramientas serán detalles de infraestructura y podrán reemplazarse cuando sea necesario.

## 4. Estructura inicial propuesta

La solución estará organizada inicialmente en cuatro proyectos:

### ParedesStarterKit.Domain

Contendrá:

- Entidades.
- Enumeraciones.
- Reglas esenciales del dominio.
- Excepciones propias del dominio.
- Objetos de valor cuando sean necesarios.

No dependerá de los demás proyectos.

### ParedesStarterKit.Application

Contendrá:

- Casos de uso.
- Interfaces necesarias para ejecutar los casos de uso.
- Modelos de entrada y salida.
- Validaciones de aplicación.
- Servicios de aplicación.

Dependerá de `Domain`.

### ParedesStarterKit.Infrastructure

Contendrá:

- Entity Framework Core.
- SQL Server.
- Implementaciones de persistencia.
- Servicios de correo.
- Almacenamiento de archivos.
- Logging técnico.
- Integraciones externas.

Dependerá de `Application` y `Domain`.

### ParedesStarterKit.Web

Contendrá:

- ASP.NET Core MVC.
- Controladores.
- Vistas.
- ViewModels.
- Configuración de autenticación.
- Inyección de dependencias.
- Archivos CSS y JavaScript.
- Interfaz administrativa.

Dependerá de `Application` e `Infrastructure`.

## 5. Dirección de las dependencias

La dirección inicial será:

```text
Web ───────────────► Application ─────────► Domain
 │                         ▲
 └────► Infrastructure ────┘