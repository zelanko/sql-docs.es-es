---
title: Novedades de SSMA para Access(AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/14/2018
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: a24d3fc0-6911-4bfa-828a-197abf222e02
caps.latest.revision: 37
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: b3fba0ce4efe8f168aa06aa27adb350d4d288dc6
ms.sourcegitcommit: fb269accc3786715c78f8b6e2ec38783a6eb63e9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2018
ms.locfileid: "40396572"
---
# <a name="whats-new-in-ssma-for-access-accesstosql"></a>Novedades de SSMA para Access (AccessToSQL)
En este artículo se enumera SSMA para los cambios de acceso en cada versión.  

## <a name="ssma-v79"></a>SSMA v7.9
La versión v7.9 de SSMA para Access contiene los siguientes cambios:
- Correcciones de destino que mejoran las métricas de calidad y la conversión.
- Soporte técnico en línea de comandos SSMA para modificar la asignación de tipos de datos y las preferencias del proyecto.
- El cuadro de diálogo de conexión de Azure SQL Database de SSMA también se ha modificado para especificar el nombre completo del servidor. En versiones anteriores de SSMA, el prefijo de la base de datos de SQL Azure se tenía que se menciona explícitamente dentro de la configuración de proyectos.

> [!IMPORTANT]
> Con SSMA v7.4 y versiones posteriores, .net 4.5.2 es un requisito previo de instalación.

## <a name="ssma-v78"></a>SSMA v7.8
La versión v7.8 de SSMA para Access contiene los siguientes cambios:
- Asignación de tipo de cambio resaltado en la configuración del proyecto.
- Proporciona la capacidad de los usuarios deshabilitar la telemetría.

> [!IMPORTANT]
> Con SSMA v7.4 y versiones posteriores, .net 4.5.2 es un requisito previo de instalación.

## <a name="ssma-v77"></a>SSMA v7.7
La versión v7.7 de SSMA para Access contiene los siguientes cambios:
- SSMA para Access se ha mejorado con correcciones de destino que mejoran las métricas de calidad y la conversión.
- Según la demanda popular, la versión de 32 bits de SSMA para Access se está hacia atrás. En comparación con la implementación anterior (anterior a v7.4), hay dos paquetes de instalador, pero no se puede instalar en paralelo. Como resultado, debe elegir la versión más adecuada en función de los componentes de conectividad que tiene. Siempre es preferible usar la versión de 64 bits, si es posible.

> [!IMPORTANT]
> Con SSMA v7.4 y versiones posteriores, .net 4.5.2 es un requisito previo de instalación.

## <a name="ssma-v76"></a>SSMA v7.6
La versión v7.6 de SSMA para Access se ha mejorado con correcciones de destino que mejoran la calidad y la conversión de las métricas y con compatibilidad con SQL Server 2017 (versión preliminar pública). Compatibilidad con SQL Server 2017 en Windows y Linux en versión preliminar pública y no debe usarse para las migraciones de producción.

> [!IMPORTANT]
> Con SSMA v7.4 y versiones posteriores, .net 4.5.2 es un requisito previo de instalación y se ha dejado de usar la versión de 32 bits de la herramienta.

## <a name="ssma-v75"></a>SSMA v7.5
La versión 7.5 de SSMA para Access se ha mejorado con varias mejoras para garantizar mayor accesibilidad para personas con discapacidades.

> [!IMPORTANT]
> .NET 4.5.2 es un requisito previo para la instalación de SSMA v7.5. Además, a partir de v7.4, la versión de 32 bits de SSMA está en desuso.

## <a name="ssma-v74"></a>SSMA v7.4
La versión v7.4 de SSMA para Access contiene los siguientes cambios:
- El **tiempo de espera de consulta** opción ahora está disponible durante la detección de objetos de esquema de origen y destino.
![opción de tiempo de espera de consulta](../media/query-timeout_red.png)

- La métrica de calidad y la conversión se ha mejorado con correcciones de destino, según los comentarios recibidos.

> [!IMPORTANT]
> .NET 4.5.2 es un requisito previo para la instalación de SSMA v7.4. Además, a partir de v7.4, la versión de 32 bits de SSMA está en desuso.

## <a name="ssma-v73"></a>SSMA v7.3
La versión v7.3 de SSMA para Access contiene los siguientes cambios:
- Métrica de calidad y la conversión mejorada con correcciones de destino según los comentarios recibidos.
- Marco de extensibilidad SSMA expuesta a través de los siguientes elementos:
  - Funcionalidad de exportación a un proyecto de SQL Server Data Tools (SSDT).
    -   Ahora puede exportar las secuencias de comandos de esquema de SSMA para un proyecto de SSDT. Puede usar los scripts de esquema para realizar cambios de esquema adicional e implementar la base de datos.
![Guardar como comando de proyecto SSDT](../media/export-schema-scripts_red.png)

  - Bibliotecas que pueden utilizarse en SSMA para realizar conversiones personalizadas.
    - Ahora se puede crear código que pueda controlar las conversiones de sintaxis personalizada y las conversiones que antes no estaban controlaba SSMA.
      - Las instrucciones sobre cómo construir un convertidor personalizado están disponibles en esta entrada de blog, [funciones de conversión de ampliación de SQL Server Migration Assistant](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/).
      - Proyecto de ejemplo para la conversión se puede descargar este [entrada de blog](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/).

## <a name="ssma-v72"></a>SSMA v7.2
La versión v7.2 de SSMA para Access contiene los siguientes cambios:
- Métrica de calidad y la conversión mejorada con correcciones de destino según los comentarios recibidos.
- Mejoras de telemetría para proporcionar una mejor puntos de datos para solucionar problemas de los clientes y mejorar las tasas de conversión de SSMA.

## <a name="ssma-v71"></a>SSMA v7.1
La versión 7.1 de SSMA para Access contiene los siguientes cambios:
- SQL Server 2017 en Windows y Linux CTP1 ahora es una plataforma de destino admitida para la migración. Esta característica está en versión preliminar técnica y admite el movimiento de datos y el esquema para servidores SQL Server de destino.
- SSMA ahora es compatible con las actualizaciones automáticas para descargar la versión más reciente de SSMA en cuanto está disponible.
- Archivos binarios de instalación de SSMA ahora se entregan a través de los archivos de paquete de Windows installer (.msi).

**Recursos**

[Funciones de conversión de SQL Server Migration Assistant de ampliación](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)
  
## <a name="may-2016"></a>Mayo de 2016  
La versión de mayo de 2016 de SSMA para Access contiene los siguientes cambios:  
  
-  Se agregó compatibilidad oficial para SQL Server 2016
-  Quitar la comprobación de instalador para .net 2.0.
-  Se ha corregido "guardar el proyecto" y "open project" comandos para la consola SSMA.
-  Se ha corregido el comando "securepassword" para la consola SSMA.
-  Se ha corregido el recuento de objetos para la carga inicial.
-  Se ha corregido la carga para las pestañas de la interfaz de usuario para el acceso de datos de tablas.
-  Se corrigió el error en la configuración global. 
   
## <a name="march-2016"></a>Marzo de 2016  
La versión de vista previa de marzo de 2016 de SSMA para Access contiene los siguientes cambios:  
  
-  Se agregó compatibilidad para la migración a SQL Server 2016.  
   
## <a name="january-2016"></a>Enero de 2016  
La versión de mantenimiento de enero de 2016 de SSMA para Access contiene los siguientes cambios:  
  
-  Fijo función no válida para el valor predeterminado de un campo GUID (RFC 3894811).  
-  Bloqueo fijo en la importación de registros a SQL Database (Azure) (RFC 4919573).  
-  La vista se ha agregado el elemento de menú de registro para SSMA (RFC 5706203).  
-  Se ha agregado telemetría.  
  
## <a name="july-2014"></a>Julio de 2014  
La versión de julio de 2014 de SSMA para Access contiene los siguientes cambios:  
  
-   Conversión de código de Azure SQL DB mejorada.  
-   Mover la funcionalidad del módulo de extensión al esquema para admitir la base de datos de SQL Azure.  
-   Mejoras de rendimiento probadas para bases de datos con objetos de más de 10 KB.  
-   Se ha agregado mejoras de interfaz de usuario para tratar con un gran número de objetos.  
-   Se agregó compatibilidad para el resaltado de esquemas LOB "conocidos" (por lo que se pueden omitir en la conversión).  
-   Mejoras de velocidad de conversión se ha agregado.
-   Se ha agregado compatibilidad para mostrar el objeto de cuenta en la interfaz de usuario.
-   Tamaño del informe reducida en más del 25%.
-   Mensajes de error mejorados para construcciones sin analizar.  
  
## <a name="april-2014"></a>Abril de 2014  
La versión de abril de 2014 de SSMA para Access contiene los siguientes cambios:  
  
-   Se agregó compatibilidad para MS SQL Server 2014.  
-   Errores corregidos con respecto a la conversión a Azure.  
-   Errores corregidos con respecto a las páginas de informe invisible en Internet Explorer 10.  
  
## <a name="january-2012"></a>Enero de 2012  
La versión de enero de 2012 de SSMA para Access contiene los siguientes cambios:  
  
-   Proporciona la opción no se conserva username y password por MS Access vinculado tablas después de la migración.  
-   Establezca las acciones en cascada para las referencias circulares a ninguna acción.  
-   Siempre que se han establecido los mensajes apropiados que indica las acciones en cascada para las referencias circulares a ninguna acción.  
  
## <a name="july-2011"></a>Julio de 2011  
La versión de julio de 2011 de SSMA para Access contiene los siguientes cambios:  
  
-   Durante la migración de datos de informes de errores mejorado.  
  
## <a name="april-2011"></a>Abril de 2011  
La versión de abril de 2011 de SSMA para Access contiene los siguientes cambios:  
  
-   Agrega una sola instalable de "SSMA para Access", que es compatible con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali" y SQL Azure.  
-   Agrega la posibilidad de conectar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali".  
-   Se ha agregado SSMA para la versión de la consola de acceso admite por compatibilidad con versiones anteriores. Puede abrir los proyectos creados con versiones anteriores a v5.0 SSMA.
-   Agrega la capacidad de instalar el producto de v5.0 SSMA en paralelo (SxS) con las versiones anteriores del producto SSMA.  
  
## <a name="july-2010"></a>Julio de 2010  
La versión de julio de 2010 de SSMA para Access contiene los siguientes cambios:  
  
-   Se agregó compatibilidad para migrar a SQL Server 2008 R2 y SQL Azure.
-   Agrega una conexión segura a SQL Server y SQL Azure.  
-   Se agregó compatibilidad para bases de datos de Access 2010.
-   Agrega una nueva aplicación de consola de SSMA para la ejecución de línea de comandos.
-   Se agregó compatibilidad para el tipo de datos DateTime2 de SQL Server.
  
## <a name="june-2008"></a>Junio de 2008  
La versión de junio de 2008 de SSMA para Access contiene los siguientes cambios:  
  
-   Se agregó compatibilidad para bases de datos de Access 2007.  
  
## <a name="may-2007"></a>Mayo de 2007  
La versión de mayo de 2007 de SSMA para Access contiene los siguientes cambios:  
  
-   Se agregó compatibilidad para bases de datos de Access que usen directivas de grupo de trabajo.  
-   Proporciona la capacidad de eliminar los objetos convertidos desde el Explorador de metadatos de SQL Server.  
-   Se agregó compatibilidad para comentarios escritos por el usuario en el servidor SQL Server tiene un formato de modo de SQL.  
-   Se ha agregado mejoras en la conversión de objetos.  
  
## <a name="november-2006"></a>Noviembre de 2006  
La versión de noviembre de 2006 de SSMA para Access contiene los siguientes cambios:  
  
-   Agrega un Asistente para migración de nueva base de datos que le guiará a través de la migración de una sola base de datos de Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
-   Agrega una nueva conversión, carga, y el comando Migrate que convierte las bases de datos de Access, carga los objetos convertidos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], y migra los datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] todo en un paso.  
-   Migración de consultas mejorado. Migración de consulta ahora se convierte más consultas a las vistas de selección. Para obtener más información, consulte [convertir objetos de base de datos de Access](converting-access-database-objects-accesstosql.md).  
-   Se agregó la capacidad de editar las propiedades de tabla e índice en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **tabla** ficha.  
-   Agregar nueva configuración global:  
    -   Puede optar por mostrar los números de línea en las ventanas del editor.  
    -   Puede configurar SSMA para preguntar si desea para reemplazar objetos duplicados, o siempre o nunca reemplazar objetos duplicados durante la conversión de esquema.  
-   Agrega una nueva opción de conversión que le permite especificar si SSMA muestra una advertencia cuando una consulta compleja contiene un carácter comodín.  
  
## <a name="july-2006"></a>Julio de 2006  
La versión de julio de 2006 de SSMA para Access fue la versión inicial.
