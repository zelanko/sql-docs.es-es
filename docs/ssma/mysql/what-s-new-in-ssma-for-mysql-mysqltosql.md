---
title: "¿Qué &#39; s de SSMA para MySQL (MySQLToSql) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 1451a0b0-6713-4d0c-954f-ea3d8fce1d31
caps.latest.revision: 21
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 42706f2ce71fc540d8538f9614f1db17b4f70ea7
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="what39s-new-in-ssma-for-mysql-mysqltosql"></a>¿Qué &#39; s de SSMA para MySQL (MySQLToSql)
Este tema enumeran SSMA para cambios de MySQL en cada versión.  

## <a name="may-2016"></a>Mayo de 2016  
La versión de mayo de 2016 de SSMA para MySQL contiene los siguientes cambios:.

1.  Ha agregado compatibilidad con SQL Server 2016
2.  Resolución y analizador mejorada
3.  Quita la comprobación de instalador para .net 2.0
4.  Dependencias de módulo de extensión actualizado respecto a .net 3.5 a .net 4.0
5.  Valor predeterminado fijo BigInt typemapping para MySql
6.  Fija "guardar el proyecto" y "Abrir proyecto" comandos de consola SSMA
7.  Comando "securepassword" fijo para la consola de SSMA
8.  Corregido el recuento de objetos para la carga inicial
9.  Objetos MsSql fijos cargar
10. Ha corregido el error en la configuración global 
 
## <a name="march-2016"></a>Marzo de 2016  
La versión de vista previa de marzo de 2016 de SSMA para MySQL contiene los siguientes cambios:  
  
1.  Admite la migración a SQL Server 2016  
  
## <a name="january-2016"></a>Enero de 2016  
La versión de mantenimiento de enero de 2016 de SSMA para MySQL contiene los siguientes cambios:  
  
1.  Elemento de menú de registro de la vista agregada para SSMA (RFC 5706203)  
  
2.  Telemetría agregada  
  
## <a name="july-2014"></a>Julio de 2014  
La versión de julio de 2014 de SSMA para MySQL contiene los siguientes cambios:  
  
1.  Conversión de código de base de datos de SQL Azure mejorada  
  
2.  Funcionalidad del módulo de extensión movida al esquema para admitir la base de datos de SQL Azure  
  
3.  Mejoras de rendimiento que comprueba si hay bases de datos con más de 10k objetos  
  
4.  Mejoras de la interfaz de usuario para tratar con un gran número de objetos  
  
5.  Resaltado de esquemas LOB "conocidos" (de manera que puede hacer caso omiso de conversión)  
  
6.  Mejoras de velocidad de conversión  
  
7.  Mostrar recuentos de objetos de interfaz de usuario  
  
8.  Reducción del tamaño de informes en más del 25%  
  
9. Mensajes de error mejorados para estructuras sin analizar.  
  
## <a name="april-2014"></a>Abril de 2014  
La versión de julio de 2011 de SSMA para MySQL contiene los siguientes cambios:  
  
1.  Se agregó compatibilidad de MS SQL Server 2014.  
  
2.  Los errores corregidos en relación con la conversión a Azure  
  
3.  Los errores corregidos en relación con páginas de informe invisible en Internet Explorer 10.  
  
## <a name="july-2011"></a>Julio de 2011  
La versión de julio de 2011 de SSMA para MySQL contiene los siguientes cambios:  
  
-   Admite la conversión de límite en cuanto al [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] desplazamiento "Denali".  
  
-   Notificación durante la migración de datos de errores mejorada.  
  
## <a name="april-2011"></a>Abril de 2011  
La versión de abril de 2011 de SSMA para MySQL contiene los siguientes cambios:  
  
-   Único instalable de "SSMA para MySQL", que es compatible con [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali" y SQL Azure.  
  
-   La capacidad de conectar [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali".  
  
-   Motor de migración de datos de lado cliente, admitir la migración de paralelo de datos ha mejorado.  
  
-   Rendimiento de la migración de datos mejorada con simples y de forma masiva registra los modelos de recuperación.  
  
-   SSMA para la versión de la consola de MySQL admite compatibilidad con versiones anteriores. Podrá abrir los proyectos creados con versiones anteriores a v5.0 SSMA.  
  
-   SSMA para MySQL v5.0 producto puede ser instalado en paralelo (SxS) con las versiones anteriores del producto SSMA.  
  
## <a name="july-2010"></a>Julio de 2010  
La versión de julio de 2010 de SSMA para MySQL contiene las siguientes características:  
  
1.  **Mejoras en la interfaz de usuario:**  
  
    -   Pestaña "Modos de SQL" para los objetos de base de datos MySQL  
  
    -   Ficha "Configuración" para los objetos de base de datos MySQL  
  
    -   Pestaña de "Datos" para las tablas de MySQL  
  
    -   Configuración del proyecto actualizado en la conversión y páginas de migración  
  
    -   "Configuración de migración de datos" en el nivel de tabla  
  
2.  **Mejoras para conectarse a SQL Server y MySQL:**  
  
    -   Conectividad SSL de MySQL  
  
    -   Cifrado conectividad en SQL Server  
  
3.  **Mejoras en el Explorador de Metabase de MySQL:**  
  
    -   Cargar todos los objetos de base de datos MySQL y sus respectivas fichas.  
  
4.  **Mejoras en la conversión de objetos:**  
  
    -   Conversión de objetos de la MySQL Metabase, procedimientos, funciones, vistas, desencadenadores y las instrucciones.  
  
    -   Compatibilidad limitada para los tipos de datos espaciales en tablas.  
  
    -   Opción para convertir las funciones de MySQL a procedimientos almacenados de SQL Server  
  
    -   Opción para aplicar la asignación de conjunto de caracteres y modos de SQL durante la conversión de objetos  
  
5.  **Mejoras en la migración de datos:**  
  
    -   Compatibilidad para migración de datos mediante el servidor y motores de migración de datos de lado cliente  
  
    -   Compatibilidad con la migración de datos espaciales  
  
    -   SQL personalizada para la migración de datos para tablas  
  
6.  **SSMA para la consola de MySQL:**  
  
    -   Compatibilidad con características de consola SSMA para MySQL  
  
    -   Compatibilidad para crear una interfaz de nivel de Script  
  
## <a name="january-2010"></a>Enero de 2010  
La versión de enero de 2010 de SSMA para MySQL fue la versión inicial. Contiene las siguientes características:  
  
-   Se admite la migración a local SQL Server y SQL Azure.  
  
-   **Característica de instantánea:** migración de datos y esquema de MySQL tablas o índices y restricciones.  
  

