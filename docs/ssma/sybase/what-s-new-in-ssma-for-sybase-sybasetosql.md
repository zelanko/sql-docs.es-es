---
title: "¿Qué &#39; s de SSMA para SAP ASE (SybaseToSQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 09/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 2be0cf8d-6dbe-443a-abbd-036249922205
caps.latest.revision: 21
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: e3c781449a8f7a1b236508cd21b8c00ff175774f
ms.openlocfilehash: 91c748f24b360934e160cea8b03c2c2259766a5c
ms.contentlocale: es-es
ms.lasthandoff: 09/30/2017

---
# <a name="what39s-new-in-ssma-for-sap-ase-sybasetosql"></a>¿Qué &#39; s de SSMA para SAP ASE (SybaseToSQL)
Este tema enumeran SSMA para cambios de SAP ASE (anteriormente SSMA para Sybase) en cada versión. 

## <a name="ssma-v76"></a>SSMA v7.6
La versión de v7.6 de SSMA para SAP ASE contiene los siguientes cambios:
- SSMA para SAP ASE se ha mejorado con correcciones de destino que mejoran las métricas de calidad y la conversión y con el soporte para SQL Server 2017 (vista previa pública). Compatibilidad con SQL Server 2017 en Windows y Linux se encuentra en versión preliminar pública y no debe usarse para las migraciones de producción.
- SSMA para SAP ASE se ha actualizado para proporcionar compatibilidad para la conversión de funciones de Sybase.

> [!IMPORTANT]
> Con SSMA v7.4 y versiones posteriores, .net 4.5.2 es un requisito previo de instalación y se ha cancelado la versión de 32 bits de la herramienta.

## <a name="ssma-v75"></a>SSMA 7.5
La versión 7.5 de SSMA para SAP ASE contiene los siguientes cambios:
-   Mejorado con varias mejoras para garantizar una mayor accesibilidad para personas con discapacidades.
-   Se actualizaron para proporcionar compatibilidad para crear o reemplazar la sintaxis.

> [!IMPORTANT]
> .NET 4.5.2 es un requisito previo para la instalación de SSMA 7.5. Además, a partir de v7.4, la versión de 32 bits de SSMA se está suspendida.  

## <a name="ssma-v74"></a>SSMA v7.4
La versión v7.4 de SSMA para Sybase contiene los siguientes cambios:
- El **tiempo de espera de consulta** opción ahora está disponible durante la detección de objetos de esquema en el origen y de destino.
![opción de tiempo de espera de consulta](../media/query-timeout_red.png)
- La métrica de calidad y la conversión se ha mejorado con correcciones de destino, en función de los comentarios de clientes.

> [!IMPORTANT]
> .NET 4.5.2 es un requisito previo para la instalación de SSMA v7.4. Además, a partir de v7.4, la versión de 32 bits de SSMA se está suspendida.  

## <a name="ssma-v73"></a>SSMA v7.3
La versión v7.3 de SSMA para Sybase contiene los siguientes cambios:
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
La versión de v7.2 de SSMA para Sybase contiene los siguientes cambios:
- Métrica de calidad y la conversión mejorada con correcciones de destino en función de los comentarios de clientes.
- Mejoras de telemetría para proporcionar una mejor puntos de datos para solucionar problemas de los clientes y mejorar las tasas de conversión de SSMA.

## <a name="ssma-v71"></a>SSMA v7.1
La versión 7.1 de SSMA para Access contiene los siguientes cambios:
- 2017 de SQL Server en Windows y Linux CTP1 ahora es una plataforma de destino admitida para la migración. Esta característica está en versión preliminar técnica y soporta el movimiento de datos y el esquema para servidores SQL Server de destino.
- SSMA ahora es compatible con las actualizaciones automáticas para descargar la versión más reciente de SSMA tan pronto como está disponible.
- Archivos binarios de instalación de SSMA ahora se entregan a través de los archivos de paquete de Windows installer (.msi).

**Recursos**

[Amplía las capacidades de SQL Server Migration Assistant conversión](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)

[Evaluar y migrar datos de plataformas de datos no sean de Microsoft para SQL Server *(con el ejemplo de Oracle)*](https://blogs.msdn.microsoft.com/datamigration/2016/11/16/sql-server-migration-assistant-how-to-assess-and-migrate-databases-from-non-microsoft-data-platforms-to-sql-server/) 

## <a name="may-2016"></a>Mayo de 2016  
La versión de mayo de 2016 de SSMA para Sybase contiene los siguientes cambios:  

-  Se agregó compatibilidad para SQL Server 2016.
-  Quita la comprobación de instalador para .net 2.0.
-  Dependencia del módulo de extensión actualizada desde .net 3.5 a .net 4.0.
-  Fija "guardar el proyecto" y "Abrir proyecto" comandos de consola SSMA.
-  Se ha corregido "securepassword" comando de consola SSMA.
-  Se ha corregido el recuento de objetos para la carga inicial.
-  Ha corregido el error en configuración global.

## <a name="march-2016"></a>Marzo de 2016  
La versión de vista previa de marzo de 2016 de SSMA para Sybase contiene los siguientes cambios:  
  
-  Se agregó compatibilidad para la migración a SQL Server 2016.  
  
## <a name="january-2016"></a>Enero de 2016  
La versión de mantenimiento de enero de 2016 de SSMA para Sybase contiene los siguientes cambios:  
  
-  Vista ha agregado el elemento de menú de registro para SSMA (RFC 5706203).  
-  Telemetría agregada. 
  
## <a name="july-2014"></a>Julio de 2014  
La versión de julio de 2014 de SSMA para Sybase contiene los siguientes cambios:  
  
-  Conversión de código de base de datos de SQL Azure mejorada.  
-  Mover la funcionalidad del módulo de extensión al esquema para admitir la base de datos de SQL Azure.  
-  Mejoras de rendimiento agregado habían probado para bases de datos con más de 10k objetos.  
-  Mejoras de interfaz de usuario agregadas para tratar con un gran número de objetos.  
-  Agrega la capacidad para resaltar "conocidos" esquemas LOB (por lo que pueden hacer caso omiso de conversión).  
-  Agrega mejoras de velocidad de conversión.  
-  Agrega la capacidad para mostrar recuentos de objetos de interfaz de usuario. 
-  Tamaño del informe reducido por más de 25%.  
-  Mensajes de error mejorados para estructuras sin analizar.  
  
## <a name="april-2014"></a>Abril de 2014  
La versión de abril de 2014 de SSMA para Sybase contiene los siguientes cambios:  
  
-   Se agregó compatibilidad de MS SQL Server 2014.  
-   Los errores corregidos en relación con la conversión a Azure.  
-   Los errores corregidos en relación con páginas de informe invisible en Internet Explorer 10.  
  
## <a name="january-2012"></a>Enero de 2012  
La versión de enero de 2012 de SSMA para Sybase contiene los siguientes cambios:  
  
-   Se agregó compatibilidad para la conversión de desencadenador de reversión.  
-   Proporciona corrección para convertir@ROWCOUNT y @@ERROR en la misma instrucción de conjunto.  
  
## <a name="july-2011"></a>Julio de 2011  
La versión de julio de 2011 de SSMA para Sybase contiene los siguientes cambios:  
  
-   Notificación durante la migración de datos de errores mejorada.  
  
## <a name="april-2011"></a>Abril de 2011  
La versión de abril de 2011 de SSMA para Sybase contiene los siguientes cambios:  
  
-   Producto "SSMA para Sybase" consolidado, que es compatible con [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali" y SQL Azure.  
-   Agrega compatibilidad para la conexión y migración a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali".  
-   Agrega una nueva característica para convertir y migrar las bases de datos de Sybase a SQL Azure.  
-   Motor de migración de datos de cliente mejorado, admitir la migración de paralelo de datos.  
-   Rendimiento de la migración de datos mejorada con simples y de forma masiva registra los modelos de recuperación.  
-   Agrega la capacidad para convertir correctamente y migrar bases de datos de Sybase distingue mayúsculas de minúsculas a mayúsculas y minúsculas de SQL Server.  
-   Ha agregado compatibilidad para la conversión de instrucciones de combinación no ANSI de Sybase ASE a las instrucciones de combinación ANSI de SQL Server se ha ampliado para eliminar y actualizar las instrucciones.  
-   Proporciona opciones de conectividad adicionales para conectarse a servidores de Sybase ASE usando el proveedor de ODBC para Sybase ASE y proveedores de Sybase ASE ADO.Net.  
-   Quita la dependencia de una base de datos independiente denominada **SysDB**, que contiene las funciones de emulación de Sybase (que se instala como parte del paquete de extensión).  
-   Agrega la capacidad para instalar SSMA para Sybase: paquete de extensión en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] clústeres.  
-   Ha agregado compatibilidad con versiones anteriores de proyectos creados con versiones anteriores de SSMA (v4.0 y v4.2).  
-   Agrega la capacidad para instalar SSMA para Sybase v5.0 producto side-by-side (SxS) con las versiones anteriores de SSMA (v4.0 y v4.2).  
  
## <a name="july-2010"></a>Julio de 2010  
La versión de julio de 2010 de SSMA para Sybase contiene los siguientes cambios:  
  
-   Se agregó compatibilidad para migrar a SQL Server 2008 R2.  
-   Agrega una nueva aplicación de consola de SSMA para la ejecución de línea de comandos.  
-   Se agregó compatibilidad para la migración de datos mediante motores de migración de datos de cliente y servidor.  
-   Se agregó compatibilidad para la instrucción de "SELECT" personalizado"en la migración de datos.  
-   Se agregó compatibilidad para la migración de Sybase ASE 15.0.3 y 15,5.  
  
## <a name="june-2008"></a>Junio de 2008  
La versión de junio de 2008 de SSMA para Sybase contiene los siguientes cambios:  
  
-   Agregado SSMA evaluador, que se prueba automáticamente la conversión del objeto de base de datos y la migración de datos realizadas por SSMA. Después de que haya finalizado todos los pasos de migración de SSMA, use SSMA evaluador para comprobar que los objetos convertidos funcionan del mismo modo y que todos los datos se transfirió correctamente.  
-   Ha agregado la conversión anterior a SQL. Usuario puede especificar ahora una tabla temporal (y otro objeto) declaraciones para cada procedimiento de origen que se usará en la conversión.  
-   Mejoras agregadas en la conversión de objetos:  
    -   Une conversión revisado.  
    -   Agregados y no agregados sin necesidad de/agrupar por cláusulas.  
    -   La función IDENTITY con una instrucción SELECT INTO.  
    -   Restricciones en clúster y los índices de datos solo bloqueado.  
    -   Tablas temporales creadas por SELECT INTO.  
    -   Las restricciones o índices para las tablas temporales.  
    -   Nueva [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] se admiten los tipos de fecha y hora de 2008.  
    -   Compatibilidad de conectividad y los tipos de datos de Sybase 15.0.  
  
## <a name="may-2007"></a>Mayo de 2007  
La versión de mayo de 2007 de SSMA para Sybase contiene los siguientes cambios:  
  
-   Agrega la capacidad para cargar el contenido de la base de datos más rápidamente cuando se guarda un proyecto.  
-   Ha agregado compatibilidad para comentarios introducidos por el usuario en el servidor SQL Server con el formato modo SQL.  
-   Mejoras agregadas en la conversión de objetos.  
  
No se actualizó el archivo de ayuda para esta versión. Para obtener más información, vea la sección Notas de la documentación más adelante en este tema.  
  
## <a name="november-2006"></a>Noviembre de 2006  
La versión de noviembre de 2006 de SSMA para Sybase contiene los siguientes cambios:  
  
-   Agrega nuevos valores globales:  
    -   Puede optar por mostrar números de línea en las ventanas del editor.  
    -   Puede configurar SSMA para preguntar si desea para reemplazar objetos duplicados o siempre o nunca reemplazar objetos duplicados durante la conversión de esquema.  
-   Agrega una nueva opción de conversión que le permite configurar la forma SSMA controla las siguientes situaciones:  
    -   Una instrucción CAST o CONVERT que contiene una cadena binaria.  
    -   Comprueba si hay valores null en expresiones de igualdad.  
    -   Tablas de proxy.  
    -   Números de error de mensaje de usuario por RAISERROR.  
    -   Instrucciones UPDATE que contienen identificadores sin resolver.  
-   Agrega una nueva opción de migración que le permite especificar cómo SSMA debe controlar las fechas que están fuera de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] intervalo de fechas.  
-   Agrega un **SQL con el formato** en el **SQL** ficha, que da formato al código para mejorar la legibilidad.  
-   Correcciones de errores que incluyen lo siguiente:  
    -   SSMA convierte ahora el bloqueo de tabla *tabla* en {SHARED | Instrucciones de modo exclusivo} mediante la adición de una sugerencia TABLOCK o TABLOCKX para la consulta SELECT subsiguientes en la tabla.  
    -   Ahora se han agregado las conversiones necesarias cuando se utilizan tipos de archivo binario en expresiones de caracteres.  
    -   Mejoras de rendimiento y memoria.  
  
## <a name="july-2006"></a>Julio de 2006  
La versión de julio de 2006 de SSMA para Sybase fue la versión inicial.  
  
## <a name="see-also"></a>Vea también  
[Introducción a SSMA para Sybase &#40; SybaseToSQL &#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)
