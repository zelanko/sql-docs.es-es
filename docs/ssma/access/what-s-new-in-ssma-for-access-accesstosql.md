---
title: Novedades de SSMA para Access(AccessToSQL) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-access
ms.custom: 
ms.date: 09/22/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: a24d3fc0-6911-4bfa-828a-197abf222e02
caps.latest.revision: "37"
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e82bc510cb99d5666fa9413ac6212491041b568d
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="whats-new-in-ssma-for-access-accesstosql"></a>Novedades de SSMA para Access (AccessToSQL)
En este tema se enumera SSMA de cambios de acceso en cada versión.  

## <a name="ssma-v76"></a>SSMA v7.6
La versión v7.6 de SSMA para Access se ha mejorado con correcciones de destino que mejoran las métricas de calidad y la conversión y con el soporte para SQL Server 2017 (vista previa pública). Compatibilidad con SQL Server 2017 en Windows y Linux se encuentra en versión preliminar pública y no debe usarse para las migraciones de producción.

> [!IMPORTANT]
> Con SSMA v7.4 y versiones posteriores, .net 4.5.2 es un requisito previo de instalación y se ha cancelado la versión de 32 bits de la herramienta.

## <a name="ssma-v75"></a>SSMA 7.5
La versión 7.5 de SSMA para Access se ha mejorado con varias mejoras para garantizar una mayor accesibilidad para personas con discapacidades.

> [!IMPORTANT]
> .NET 4.5.2 es un requisito previo para la instalación de SSMA 7.5. Además, a partir de v7.4, la versión de 32 bits de SSMA se está suspendida.

## <a name="ssma-v74"></a>SSMA v7.4
La versión v7.4 de SSMA para Access contiene los siguientes cambios:
- El **tiempo de espera de consulta** opción ahora está disponible durante la detección de objetos de esquema en el origen y de destino.
![opción de tiempo de espera de consulta](../media/query-timeout_red.png)

- La métrica de calidad y la conversión se ha mejorado con correcciones de destino, en función de los comentarios de clientes.

> [!IMPORTANT]
> .NET 4.5.2 es un requisito previo para la instalación de SSMA v7.4. Además, a partir de v7.4, la versión de 32 bits de SSMA se está suspendida.

## <a name="ssma-v73"></a>SSMA v7.3
La versión v7.3 de SSMA para Access contiene los siguientes cambios:
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
La versión v7.2 de SSMA para Access contiene los siguientes cambios:
- Métrica de calidad y la conversión mejorada con correcciones de destino en función de los comentarios de clientes.
- Mejoras de telemetría para proporcionar una mejor puntos de datos para solucionar problemas de los clientes y mejorar las tasas de conversión de SSMA.

## <a name="ssma-v71"></a>SSMA v7.1
La versión 7.1 de SSMA para Access contiene los siguientes cambios:
- 2017 de SQL Server en Windows y Linux CTP1 ahora es una plataforma de destino admitida para la migración. Esta característica está en versión preliminar técnica y soporta el movimiento de datos y el esquema para servidores SQL Server de destino.
- SSMA ahora es compatible con las actualizaciones automáticas para descargar la versión más reciente de SSMA tan pronto como está disponible.
- Archivos binarios de instalación de SSMA ahora se entregan a través de los archivos de paquete de Windows installer (.msi).

**Recursos**

[Amplía las capacidades de SQL Server Migration Assistant conversión](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)
  
## <a name="may-2016"></a>Mayo de 2016  
La versión de mayo de 2016 de SSMA para Access contiene los siguientes cambios:  
  
-  Ha agregado compatibilidad con oficial de SQL Server 2016
-  Quita la comprobación de instalador para .net 2.0.
-  Fija "guardar el proyecto" y "Abrir proyecto" comandos de consola SSMA.
-  Se ha corregido "securepassword" comando de consola SSMA.
-  Se ha corregido el recuento de objetos para la carga inicial.
-  Carga de datos de tablas fijo para las pestañas de la interfaz de usuario para el acceso.
-  Ha corregido el error en configuración global. 
   
## <a name="march-2016"></a>Marzo de 2016  
La versión de vista previa de marzo de 2016 de SSMA para Access contiene los siguientes cambios:  
  
-  Se agregó compatibilidad para la migración a SQL Server 2016.  
   
## <a name="january-2016"></a>Enero de 2016  
La versión de mantenimiento de enero de 2016 de SSMA para Access contiene los siguientes cambios:  
  
-  Función no válida fijo para el valor predeterminado de un campo GUID (RFC 3894811).  
-  Falta de respuesta fijo sobre la importación de registros de base de datos de SQL (Azure) (RFC 4919573).  
-  Vista ha agregado el elemento de menú de registro para SSMA (RFC 5706203).  
-  Telemetría agregada.  
  
## <a name="july-2014"></a>Julio de 2014  
La versión de julio de 2014 de SSMA para Access contiene los siguientes cambios:  
  
-   Conversión de código de base de datos de SQL Azure mejorada.  
-   Mover la funcionalidad del módulo de extensión al esquema para admitir la base de datos de SQL Azure.  
-   Mejoras de rendimiento probados para bases de datos con objetos de más de 10 k.  
-   Mejoras de interfaz de usuario agregadas para tratar con un gran número de objetos.  
-   Se agregó compatibilidad para resaltar de esquemas LOB "conocidos" (de manera que puede hacer caso omiso de conversión).  
-   Agrega mejoras de velocidad de conversión.
-   Se agregó compatibilidad para mostrar el objeto de cuenta en la interfaz de usuario.
-   Tamaño del informe reducido por más de 25%.
-   Mensajes de error mejorados para estructuras sin analizar.  
  
## <a name="april-2014"></a>Abril de 2014  
La versión de abril de 2014 de SSMA para Access contiene los siguientes cambios:  
  
-   Se agregó compatibilidad para MS SQL Server 2014.  
-   Los errores corregidos en relación con la conversión a Azure.  
-   Los errores corregidos en relación con páginas de informe invisible en Internet Explorer 10.  
  
## <a name="january-2012"></a>Enero de 2012  
La versión de enero de 2012 de SSMA para Access contiene los siguientes cambios:  
  
-   Proporciona la opción para no conservar username y password para MS Access tablas vinculadas después de la migración.  
-   Establecer las acciones en cascada para referencias circulares a ninguna acción.  
-   Proporcionado por el mensajes correcta que indica las acciones cascade para las referencias circulares se ha establecido en No Action.  
  
## <a name="july-2011"></a>Julio de 2011  
La versión de julio de 2011 de SSMA para Access contiene los siguientes cambios:  
  
-   Notificación durante la migración de datos de errores mejorada.  
  
## <a name="april-2011"></a>Abril de 2011  
La versión de abril de 2011 de SSMA para Access contiene los siguientes cambios:  
  
-   Agrega una sola instalable de "SSMA para Access", que es compatible con [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali" y SQL Azure.  
-   Agrega la capacidad para conectar [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali".  
-   Agregado SSMA para la versión de la consola de acceso se admite por compatibilidad con versiones anteriores. Puede abrir los proyectos creados con versiones anteriores a v5.0 SSMA.
-   Agrega la capacidad para instalar el producto de v5.0 SSMA en paralelo (SxS) con las versiones anteriores del producto SSMA.  
  
## <a name="july-2010"></a>Julio de 2010  
La versión de julio de 2010 de SSMA para Access contiene los siguientes cambios:  
  
-   Se agregó compatibilidad para migrar a SQL Server 2008 R2 y SQL Azure.
-   Agrega una conexión segura a SQL Server y SQL Azure.  
-   Se agregó compatibilidad para bases de datos de Access 2010.
-   Agrega una nueva aplicación de consola de SSMA para la ejecución de línea de comandos.
-   Ha agregado compatibilidad para el tipo de datos DateTime2 de SQL Server.
  
## <a name="june-2008"></a>Junio de 2008  
La versión de junio de 2008 de SSMA para Access contiene los siguientes cambios:  
  
-   Se agregó compatibilidad para bases de datos de Access 2007.  
  
## <a name="may-2007"></a>Mayo de 2007  
La versión de mayo de 2007 de SSMA para Access contiene los siguientes cambios:  
  
-   Se agregó compatibilidad para bases de datos de Access que usen directivas de grupo de trabajo.  
-   Proporciona la capacidad de eliminar objetos convertidos en el Explorador de metadatos de SQL Server.  
-   Ha agregado compatibilidad para comentarios introducidos por el usuario en el servidor SQL Server con el formato modo SQL.  
-   Mejoras agregadas en la conversión de objetos.  
  
## <a name="november-2006"></a>Noviembre de 2006  
La versión de noviembre de 2006 de SSMA para Access contiene los siguientes cambios:  
  
-   Agrega un nuevo Asistente de migración de base de datos que le guía a través de la migración de una base de datos de Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
-   Agrega una nueva conversión, carga, y los comandos de migración que convierte las bases de datos de Access, carga los objetos convertidos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], y migra los datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] todo en un solo paso.  
-   Migración de consultas mejorado. Ahora convierte selecciona más consultas a las vistas de consulta migración. Para obtener más información, consulte [convertir objetos de base de datos de Access](http://msdn.microsoft.com/en-us/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c).  
-   Agrega la capacidad para editar propiedades de tabla e índice en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **tabla** ficha.  
-   Agrega nuevos valores globales:  
    -   Puede optar por mostrar números de línea en las ventanas del editor.  
    -   Puede configurar SSMA para preguntar si desea para reemplazar objetos duplicados o siempre o nunca reemplazar objetos duplicados durante la conversión de esquema.  
-   Agrega una nueva opción de conversión que le permite especificar si SSMA muestra una advertencia cuando una consulta compleja contiene un carácter comodín.  
  
## <a name="july-2006"></a>Julio de 2006  
La versión de julio de 2006 de SSMA para Access fue la versión inicial.
