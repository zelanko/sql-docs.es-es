---
title: "¿Qué &#39; s de SSMA para MySQL (MySQLToSql) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 09/30/2017
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
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: e3c781449a8f7a1b236508cd21b8c00ff175774f
ms.openlocfilehash: 30529df439a1910573b2e4b8f9e1a5f21075c4d7
ms.contentlocale: es-es
ms.lasthandoff: 09/30/2017

---
# <a name="what39s-new-in-ssma-for-mysql-mysqltosql"></a>¿Qué &#39; s de SSMA para MySQL (MySQLToSql)
Este tema enumeran SSMA para cambios de MySQL en cada versión. 

## <a name="ssma-v76"></a>SSMA v7.6
Se ha mejorado la versión v7.6 de SSMA para MySQL con correcciones de destino que mejoran las métricas de calidad y la conversión y con el soporte para SQL Server 2017 (vista previa pública). Compatibilidad con SQL Server 2017 en Windows y Linux se encuentra en versión preliminar pública y no debe usarse para las migraciones de producción.

> [!IMPORTANT]
> Con SSMA v7.4 y versiones posteriores, .net 4.5.2 es un requisito previo de instalación y se ha cancelado la versión de 32 bits de la herramienta.

## <a name="ssma-v75"></a>SSMA 7.5
La versión 7.5 de SSMA para MySQL se ha mejorado con varias mejoras para garantizar una mayor accesibilidad para personas con discapacidades.

> [!IMPORTANT]
> .NET 4.5.2 es un requisito previo para la instalación de SSMA 7.5. Además, a partir de v7.4, la versión de 32 bits de SSMA se está suspendida.

## <a name="ssma-v74"></a>SSMA v7.4
La versión v7.4 de SSMA para MySQL contiene los siguientes cambios:
- El **tiempo de espera de consulta** opción ahora está disponible durante la detección de objetos de esquema en el origen y de destino.
![opción de tiempo de espera de consulta](../media/query-timeout_red.png)
- La métrica de calidad y la conversión se ha mejorado con correcciones de destino, en función de los comentarios de clientes.

> [!IMPORTANT]
> .NET 4.5.2 es un requisito previo para la instalación de SSMA v7.4. Además, a partir de v7.4, la versión de 32 bits de SSMA se está suspendida. 

## <a name="ssma-v73"></a>SSMA v7.3
La versión v7.3 de SSMA para MySQL contiene los siguientes cambios:
- Métrica de calidad y la conversión mejorada con correcciones de destino en función de los comentarios de clientes.
- Marco de extensibilidad SSMA expuesta a través de los siguientes elementos:
  - Funcionalidad de exportación a un proyecto de SQL Server Data Tools (SSDT).
    -   Ahora puede exportar las secuencias de comandos de esquema de SSMA para un proyecto de SSDT. Puede utilizar las secuencias de comandos de esquema para realizar cambios de esquema adicionales e implementar la base de datos.
![Guardar como comando de proyecto SSDT](../media/export-schema-scripts_red.png)
  - Bibliotecas que pueden utilizarse SSMA para realizar conversiones personalizadas.
    - Ahora puede construir código que puede controlar las conversiones de sintaxis personalizados y las conversiones que antes no estaban realizaba SSMA.
      - Las instrucciones sobre cómo construir un convertidor personalizado están disponibles en esta entrada de blog, [funciones de conversión del ampliación de SQL Server Migration Assistant](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/).
      - Proyecto de ejemplo para la conversión se puede descargar este [entrada de blog](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/).

## <a name="ssma-v72"></a>SSMA v7.2
La versión de v7.2 de SSMA para MySQL contiene los siguientes cambios:
- Métrica de calidad y la conversión mejorada con correcciones de destino en función de los comentarios de clientes.
- Mejoras de telemetría para proporcionar una mejor puntos de datos para solucionar problemas de los clientes y mejorar las tasas de conversión de SSMA.

## <a name="ssma-v71"></a>SSMA v7.1
La versión 7.1 de SSMA para Access contiene los siguientes cambios:
- 2017 de SQL Server en Windows y Linux CTP1 ahora es una plataforma de destino admitida para la migración. Esta característica está en versión preliminar técnica y permite el movimiento de datos y el esquema para servidores SQL Server de destino.
- SSMA ahora es compatible con las actualizaciones automáticas para descargar la versión más reciente de SSMA tan pronto como está disponible.
- Archivos binarios de instalación de SSMA ahora se entregan a través de los archivos de paquete de Windows installer (.msi).

**Recursos**

[Amplía las capacidades de SQL Server Migration Assistant conversión](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)

[Evaluar y migrar datos de plataformas de datos no sean de Microsoft para SQL Server *(con el ejemplo de Oracle)*](https://blogs.msdn.microsoft.com/datamigration/2016/11/16/sql-server-migration-assistant-how-to-assess-and-migrate-databases-from-non-microsoft-data-platforms-to-sql-server/) 

## <a name="may-2016"></a>Mayo de 2016  
La versión de mayo de 2016 de SSMA para MySQL contiene los siguientes cambios:.

-  Se agregó compatibilidad para SQL Server 2016.
-  Analizador mejorada y resolución.
-  Quita la comprobación de instalador para .net 2.0.
-  Dependencia del módulo de extensión actualizada desde .net 3.5 a .net 4.0.
-  Valor predeterminado fijo BigInt typemapping para MySql.
-  Fija "guardar el proyecto" y "Abrir proyecto" comandos de consola SSMA.
-  Se ha corregido "securepassword" comando de consola SSMA.
-  Se ha corregido el recuento de objetos para la carga inicial.
-  Cargar los objetos MsSql fijos.
-  Ha corregido el error en configuración global.
 
## <a name="march-2016"></a>Marzo de 2016  
La versión de vista previa de marzo de 2016 de SSMA para MySQL contiene los siguientes cambios:  
  
-  Se agregó compatibilidad para la migración a SQL Server 2016. 
  
## <a name="january-2016"></a>Enero de 2016  
La versión de mantenimiento de enero de 2016 de SSMA para MySQL contiene los siguientes cambios:  
  
-  Vista ha agregado el elemento de menú de registro para SSMA (RFC 5706203).  
-  Telemetría agregada.  
  
## <a name="july-2014"></a>Julio de 2014  
La versión de julio de 2014 de SSMA para MySQL contiene los siguientes cambios:  
  
-  Conversión de código de base de datos de SQL Azure mejorada. 
-  Funcionalidad del módulo de extensión se movió al esquema para admitir la base de datos de SQL Azure.  
-  Mejoras de rendimiento habían probado para bases de datos con más de 10k objetos.  
-  Mejoras de la interfaz de usuario para trabajar con un gran número de objetos.  
-  El resaltado de los esquemas LOB "conocidos" (de manera que puede hacer caso omiso de conversión).  
-  Mejoras de la velocidad de conversión.  
-  Mostrar recuentos de objetos de interfaz de usuario.  
-  Reducción del tamaño de informe por más de 25%.  
-  Mensajes de error mejorados para estructuras sin analizar.  
  
## <a name="april-2014"></a>Abril de 2014  
La versión de julio de 2011 de SSMA para MySQL contiene los siguientes cambios:  
  
-  Se agregó compatibilidad de MS SQL Server 2014.  
-  Los errores corregidos en relación con la conversión a Azure  
-  Los errores corregidos en relación con páginas de informe invisible en Internet Explorer 10.  
  
## <a name="july-2011"></a>Julio de 2011  
La versión de julio de 2011 de SSMA para MySQL contiene los siguientes cambios:  
  
-   Admite la conversión de límite en cuanto al [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] desplazamiento "Denali".  
-   Notificación durante la migración de datos de errores mejorada.  
  
## <a name="april-2011"></a>Abril de 2011  
La versión de abril de 2011 de SSMA para MySQL contiene los siguientes cambios:  
  
-   Único instalable de "SSMA para MySQL", que es compatible con [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali" y SQL Azure.  
-   La capacidad de conectar [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali".  
-   Motor de migración de datos de cliente mejorado, admitir la migración de paralelo de datos.  
-   Rendimiento de la migración de datos mejorada con simples y de forma masiva registra los modelos de recuperación.  
-   SSMA para la versión de la consola de MySQL admite compatibilidad con versiones anteriores. Puede abrir los proyectos creados con versiones anteriores a v5.0 SSMA.  
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
  
    -   Soporte para la migración de datos mediante motores de migración de datos de cliente y servidor  
    -   Compatibilidad con la migración de datos espaciales  
    -   SQL personalizada para la migración de datos para tablas  
  
6.  **SSMA para la consola de MySQL:**  
  
    -   Compatibilidad con características de consola SSMA para MySQL  
    -   Compatibilidad para crear una interfaz de nivel de Script  
  
## <a name="january-2010"></a>Enero de 2010  
La versión de enero de 2010 de SSMA para MySQL fue la versión inicial. Contiene las siguientes características:  
  
-   Ha agregado compatibilidad para migración tanto local de SQL Server y SQL Azure.  
  
-   **Característica de instantánea:** migración de datos y esquema de MySQL tablas o índices y restricciones.

