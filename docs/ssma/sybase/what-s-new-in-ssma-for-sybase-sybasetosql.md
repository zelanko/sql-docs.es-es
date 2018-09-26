---
title: Novedades de SSMA para SAP ASE (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/22/2018
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 2be0cf8d-6dbe-443a-abbd-036249922205
caps.latest.revision: 21
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 3ade0baa7e970639769cf5bdba522e54d3843771
ms.sourcegitcommit: 7076fcb854c033a5dbeac7fcb22c5e15cf8528fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/19/2018
ms.locfileid: "46362039"
---
# <a name="whats-new-in-ssma-for-sap-ase-sybasetosql"></a>Novedades de SSMA para SAP ASE (SybaseToSQL)
En este artículo se enumera SSMA para SAP ASE (anteriormente SSMA para Sybase) cambios en cada versión. 

## <a name="ssma-v710"></a>SSMA v7.10
La versión de v7.10 de SSMA para SAP ASE se ha mejorado con correcciones de destino diseñadas para proporcionar seguridad adicional y protecciones de seguridad para satisfacer los cambios en los requisitos globales.

> [!IMPORTANT]
> Con SSMA v7.4 y versiones posteriores, .net 4.5.2 es un requisito previo de instalación.

## <a name="ssma-v79"></a>SSMA v7.9
La versión de v7.9 de SSMA para SAP ASE contiene los siguientes cambios:
- Correcciones de destino que mejoran las métricas de calidad y la conversión.
- Soporte técnico en línea de comandos SSMA para modificar la asignación de tipos de datos y las preferencias del proyecto.
- Soporte técnico para migrar datos mediante SQL Server Integration Services (SSIS). Después de convertir el esquema, es posible crear un paquete SSIS mediante una opción del menú contextual.
- El cuadro de diálogo de conexión de Azure SQL Database de SSMA también se ha modificado para especificar el nombre completo del servidor. En versiones anteriores de SSMA, el prefijo de la base de datos de SQL Azure se tenía que se menciona explícitamente dentro de la configuración de proyectos.

> [!IMPORTANT]
> Con SSMA v7.4 y versiones posteriores, .net 4.5.2 es un requisito previo de instalación.

## <a name="ssma-v78"></a>SSMA v7.8
La versión de v7.8 de SSMA para SAP ASE contiene los siguientes cambios:
- Asignación de tipo de cambio resaltado en la configuración del proyecto.
- Proporciona la capacidad de los usuarios deshabilitar la telemetría.

> [!IMPORTANT]
> Con SSMA v7.4 y versiones posteriores, .net 4.5.2 es un requisito previo de instalación.

## <a name="ssma-v77"></a>SSMA v7.7
La versión de v7.7 de SSMA para SAP ASE contiene los siguientes cambios:
- SSMA para SAP ASE se ha mejorado con correcciones de destino que mejoran las métricas de calidad y la conversión.
- Según la demanda popular, la versión de 32 bits de SSMA para SAP ASE es volver. En comparación con la implementación anterior (anterior a v7.4), hay dos paquetes de instalador, pero no se puede instalar en paralelo. Como resultado, debe elegir la versión más adecuada en función de los componentes de conectividad que tiene. Siempre es preferible usar la versión de 64 bits, si es posible.

> [!IMPORTANT]
> Con SSMA v7.4 y versiones posteriores, .net 4.5.2 es un requisito previo de instalación.

## <a name="ssma-v76"></a>SSMA v7.6
La versión de v7.6 de SSMA para SAP ASE contiene los siguientes cambios:
- SSMA para SAP ASE se ha mejorado con correcciones de destino que mejoran la calidad y la conversión de las métricas y con compatibilidad con SQL Server 2017 (versión preliminar pública). Compatibilidad con SQL Server 2017 en Windows y Linux en versión preliminar pública y no debe usarse para las migraciones de producción.
- SSMA para SAP ASE se actualizó para proporcionar compatibilidad para la conversión de funciones de Sybase.

> [!IMPORTANT]
> Con SSMA v7.4 y versiones posteriores, .net 4.5.2 es un requisito previo de instalación y se ha dejado de usar la versión de 32 bits de la herramienta.

## <a name="ssma-v75"></a>SSMA v7.5
La versión 7.5 de SSMA para SAP ASE contiene los siguientes cambios:
-   Mejorado con varias mejoras para garantizar mayor accesibilidad para personas con discapacidades.
-   Actualizado para proporcionar soporte técnico para crear o reemplazar la sintaxis.

> [!IMPORTANT]
> .NET 4.5.2 es un requisito previo para la instalación de SSMA v7.5. Además, a partir de v7.4, la versión de 32 bits de SSMA está en desuso.  

## <a name="ssma-v74"></a>SSMA v7.4
La versión v7.4 de SSMA para Sybase contiene los siguientes cambios:
- El **tiempo de espera de consulta** opción ahora está disponible durante la detección de objetos de esquema de origen y destino.
![opción de tiempo de espera de consulta](../media/query-timeout_red.png)
- La métrica de calidad y la conversión se ha mejorado con correcciones de destino, según los comentarios recibidos.

> [!IMPORTANT]
> .NET 4.5.2 es un requisito previo para la instalación de SSMA v7.4. Además, a partir de v7.4, la versión de 32 bits de SSMA está en desuso.  

## <a name="ssma-v73"></a>SSMA v7.3
La versión v7.3 de SSMA para Sybase contiene los siguientes cambios:
- Métrica de calidad y la conversión mejorada con correcciones de destino según los comentarios recibidos.
- Marco de extensibilidad SSMA expuesta a través de los siguientes elementos:
  - Funcionalidad de exportación a un proyecto de SQL Server Data Tools (SSDT).
    -   Ahora puede exportar las secuencias de comandos de esquema de SSMA para un proyecto de SSDT. Puede usar los scripts de esquema para realizar cambios de esquema adicional e implementar la base de datos.
![Guardar como comando de proyecto SSDT](../media/export-schema-scripts_red.png)
  - Bibliotecas que pueden utilizarse en SSMA para realizar conversiones personalizadas.
    - Ahora se puede crear código que pueda controlar las conversiones de sintaxis personalizada y las conversiones que antes no estaban controlaba SSMA.
      - Las instrucciones sobre cómo construir un convertidor personalizado están disponibles en esta entrada de blog, [funciones de conversión de ampliación de SQL Server Migration Assistant](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/).
      - Descargar un proyecto de ejemplo para la conversión de esta [entrada de blog](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/).

## <a name="ssma-v72"></a>SSMA v7.2
La versión v7.2 de SSMA para Sybase contiene los siguientes cambios:
- Métrica de calidad y la conversión mejorada con correcciones de destino según los comentarios recibidos.
- Mejoras de telemetría para proporcionar una mejor puntos de datos para solucionar problemas de los clientes y mejorar las tasas de conversión de SSMA.

## <a name="ssma-v71"></a>SSMA v7.1
La versión 7.1 de SSMA para Access contiene los siguientes cambios:
- SQL Server 2017 en Windows y Linux CTP1 ahora es una plataforma de destino admitida para la migración. Esta característica está en versión preliminar técnica y admite el movimiento de datos y el esquema para servidores SQL Server de destino.
- SSMA ahora es compatible con las actualizaciones automáticas para descargar la versión más reciente de SSMA en cuanto está disponible.
- Archivos binarios de instalación de SSMA ahora se entregan a través de los archivos de paquete de Windows installer (.msi).

**Recursos**

[Funciones de conversión de SQL Server Migration Assistant de ampliación](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)

[Evaluar y migrar datos desde las plataformas de datos que no sea Microsoft SQL Server *(con el ejemplo de Oracle)*](https://blogs.msdn.microsoft.com/datamigration/2016/11/16/sql-server-migration-assistant-how-to-assess-and-migrate-databases-from-non-microsoft-data-platforms-to-sql-server/) 

## <a name="may-2016"></a>Mayo de 2016  
La versión de mayo de 2016 de SSMA para Sybase contiene los siguientes cambios:  

-  Se agregó compatibilidad para SQL Server 2016.
-  Quitar la comprobación de instalador para .net 2.0.
-  Dependencia del módulo de extensión actualizado de .net 3.5 a .net 4.0.
-  Se ha corregido "guardar el proyecto" y "open project" comandos para la consola SSMA.
-  Se ha corregido el comando "securepassword" para la consola SSMA.
-  Se ha corregido el recuento de objetos para la carga inicial.
-  Se corrigió el error en la configuración global.

## <a name="march-2016"></a>Marzo de 2016  
La versión de vista previa de marzo de 2016 de SSMA para Sybase contiene los siguientes cambios:  
  
-  Se agregó compatibilidad para la migración a SQL Server 2016.  
  
## <a name="january-2016"></a>Enero de 2016  
La versión de mantenimiento de enero de 2016 de SSMA para Sybase contiene los siguientes cambios:  
  
-  La vista se ha agregado el elemento de menú de registro para SSMA (RFC 5706203).  
-  Se ha agregado telemetría. 
  
## <a name="july-2014"></a>Julio de 2014  
La versión de julio de 2014 de SSMA para Sybase contiene los siguientes cambios:  
  
-  Conversión de código de Azure SQL DB mejorada.  
-  Mover la funcionalidad del módulo de extensión al esquema para admitir la base de datos de SQL Azure.  
-  Mejoras de rendimiento agregado habían probado para bases de datos con más de 10k objetos.  
-  Se ha agregado mejoras de interfaz de usuario para tratar con un gran número de objetos.  
-  Agrega la capacidad de resaltar "conocidos" esquemas LOB (por lo que se pueden omitir en la conversión).  
-  Mejoras de velocidad de conversión se ha agregado.  
-  Agrega la capacidad de mostrar los recuentos de objetos en la interfaz de usuario. 
-  Tamaño del informe reducida en más del 25%.  
-  Mensajes de error mejorados para construcciones sin analizar.  
  
## <a name="april-2014"></a>Abril de 2014  
La versión de abril de 2014 de SSMA para Sybase contiene los siguientes cambios:  
  
-   Se agregó compatibilidad de MS SQL Server 2014.  
-   Errores corregidos con respecto a la conversión a Azure.  
-   Errores corregidos con respecto a las páginas de informe invisible en Internet Explorer 10.  
  
## <a name="january-2012"></a>Enero de 2012  
La versión de enero de 2012 de SSMA para Sybase contiene los siguientes cambios:  
  
-   Se agregó compatibilidad para la conversión de desencadenador de reversión.  
-   Proporciona corrección para convertir@ROWCOUNT y @@ERROR en la misma instrucción.  
  
## <a name="july-2011"></a>Julio de 2011  
La versión de julio de 2011 de SSMA para Sybase contiene los siguientes cambios:  
  
-   Durante la migración de datos de informes de errores mejorado.  
  
## <a name="april-2011"></a>Abril de 2011  
La versión de abril de 2011 de SSMA para Sybase contiene los siguientes cambios:  
  
-   Producto "SSMA para Sybase" consolidada, que es compatible con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali" y SQL Azure.  
-   Agrega compatibilidad para conectar y migrar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali".  
-   Agrega una nueva característica para convertir y migrar las bases de datos de Sybase a SQL Azure.  
-   Motor de migración mejorada de los datos del lado cliente, que admiten la migración paralela de datos.  
-   Rendimiento de la migración de datos mejorada con Simple y masiva registra los modelos de recuperación.  
-   Agrega la capacidad de convertir y migrar bases de datos de Sybase entre mayúsculas y minúsculas a mayúsculas y minúsculas de SQL Server correctamente.  
-   Se ha agregado compatibilidad para la conversión de instrucciones de combinación no ANSI de Sybase ASE a instrucciones de combinación ANSI de SQL Server se ha ampliado para eliminar y actualizar las instrucciones.  
-   Proporciona opciones de conectividad adicionales para conectarse a servidores de Sybase ASE mediante el proveedor ODBC de Sybase ASE y proveedores de ADO.Net de Sybase ASE.  
-   Quita la dependencia en una base de datos independiente denominado **SysDB**, que contiene las funciones de emulación de Sybase (instaladas como parte del paquete de extensión).  
-   Se agregó la capacidad de instalar SSMA para Sybase: paquete de extensión en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] clústeres.  
-   Se ha agregado compatibilidad con versiones anteriores de los proyectos creados con versiones anteriores de SSMA (v4.0 y v4.2).  
-   Agrega la capacidad de instalar SSMA para Sybase v5.0 producto por en paralelo (SxS) con versiones anteriores de SSMA (v4.0 y v4.2).  
  
## <a name="july-2010"></a>Julio de 2010  
La versión de julio de 2010 de SSMA para Sybase contiene los siguientes cambios:  
  
-   Se agregó compatibilidad para migrar a SQL Server 2008 R2.  
-   Agrega una nueva aplicación de consola de SSMA para la ejecución de línea de comandos.  
-   Se agregó compatibilidad para migración de datos con el servidor y motores de migración de datos del lado cliente.  
-   Se agregó compatibilidad para la instrucción "SELECT" Custom"en la migración de datos.  
-   Se agregó compatibilidad para la migración desde Sybase ASE 15.0.3 y 15.5.  
  
## <a name="june-2008"></a>Junio de 2008  
La versión de junio de 2008 de SSMA para Sybase contiene los siguientes cambios:  
  
-   Se ha agregado SSMA evaluador, que comprueba automáticamente la conversión del objeto de base de datos y la migración de datos realizadas por SSMA. Una vez finalizados todos los pasos de migración de SSMA, use el evaluador de SSMA para comprobar que los objetos convertidos funcionan del mismo modo, y que todos los datos se transfirió correctamente.  
-   Se ha agregado la conversión anterior a SQL. Usuario puede especificar ahora una tabla temporal (y otro objeto) declaraciones para cada procedimiento de origen que se usará en la conversión.  
-   Se ha agregado mejoras en la conversión de objetos:  
    -   Une la conversión revisado.  
    -   Agregados y agregados sin necesidad de/agrupar por cláusulas.  
    -   La función IDENTITY con una instrucción SELECT INTO.  
    -   Restricciones en clúster y los índices de datos solo bloqueado.  
    -   Tablas temporales creadas por SELECT INTO.  
    -   Las restricciones o índices para las tablas temporales.  
    -   Nuevo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admiten los tipos de fecha y hora de 2008.  
    -   Compatibilidad de conectividad y los tipos de datos de Sybase 15.0.  
  
## <a name="may-2007"></a>Mayo de 2007  
La versión de mayo de 2007 de SSMA para Sybase contiene los siguientes cambios:  
  
-   Agrega la capacidad para cargar el contenido de la base de datos con mayor rapidez al guardar un proyecto.  
-   Se agregó compatibilidad para comentarios escritos por el usuario en el servidor SQL Server tiene un formato de modo de SQL.  
-   Se ha agregado mejoras en la conversión de objetos.  
  
No se ha actualizado el archivo de ayuda para esta versión. Para obtener más información, vea la sección de notas de la documentación más adelante en este artículo.  
  
## <a name="november-2006"></a>Noviembre de 2006  
La versión de noviembre de 2006 de SSMA para Sybase contiene los siguientes cambios:  
  
-   Agregar nueva configuración global:  
    -   Puede optar por mostrar los números de línea en las ventanas del editor.  
    -   Puede configurar SSMA para preguntar si desea para reemplazar objetos duplicados, o siempre o nunca reemplazar objetos duplicados durante la conversión de esquema.  
-   Agrega una nueva opción de conversión que le permite configurar la forma SSMA controla las situaciones siguientes:  
    -   Una instrucción CAST o CONVERT que contiene una cadena binaria.  
    -   Comprueba si hay valores null en expresiones de igualdad.  
    -   Tablas de proxy.  
    -   Números de error de mensaje de usuario por RAISERROR.  
    -   Instrucciones UPDATE que contienen identificadores sin resolver.  
-   Agrega una nueva opción de migración que le permite especificar cómo SSMA debe controlar las fechas que están fuera de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intervalo de fechas.  
-   Agrega un **SQL con el formato** en el **SQL** ficha, que da formato al código para mejorar la legibilidad.  
-   Correcciones de errores, incluidos:  
    -   SSMA ahora convierte el bloqueo de tabla *tabla* IN {SHARED | Instrucciones de modo exclusivo} mediante la adición de una sugerencia TABLOCK o TABLOCKX a la consulta SELECT subsiguientes en la tabla.  
    -   Ahora se han agregado las conversiones necesarias cuando se usan tipos binarios en expresiones de caracteres.  
    -   Mejoras de rendimiento y memoria.  
  
## <a name="july-2006"></a>Julio de 2006  
La versión de julio de 2006 de SSMA para Sybase fue la versión inicial.  
  
## <a name="see-also"></a>Vea también  
[Introducción a SSMA para Sybase &#40;SybaseToSQL&#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)
