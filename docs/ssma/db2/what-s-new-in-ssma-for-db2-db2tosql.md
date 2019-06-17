---
title: Novedades de SSMA para DB2 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 06/11/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 1cc38f85-3caa-42d0-8c76-a380c1d15c67
author: HJToland3
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 02d320990b255cdee2a6d75ac88a93ab98ce5ff4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66841073"
---
# <a name="whats-new-in-ssma-for-db2-db2tosql"></a>Novedades de SSMA para DB2 (DB2ToSQL)

Este artículo se enumeran los cambios de DB2 en cada versión de SQL Server Migration Assistant (SSMA).

## <a name="ssma-v82"></a>SSMA v8.2

La versión v8.2 de SSMA para DB2 se ha mejorado con para solucionar problemas con las conexiones a Azure SQL Database desde la herramienta de consola SSMA y falta una columna COUNT_BIG deklaraci vistas durante la conversión. Además, esta versión incluye un conjunto de correcciones diseñado para mejorar la calidad y las métricas de conversión, así como correcciones de destino:

* Un problema con los índices no clúster deshabilitados tras la migración de datos.
* Detección de .NET Framework durante la instalación silenciosa.
* Un bloqueo intermitente que se produce cuando se descarga una nueva versión.

> [!NOTE]
> Un problema conocido con la actualización automática puede producir el error de una actualización desde SSMA v8.1 a v8.2. Si se produce este error, descargue la nueva versión e instalarlo manualmente.

> [!IMPORTANT]
> Con SSMA v7.4 y versiones posteriores, .net 4.5.2 es un requisito previo de instalación.

## <a name="ssma-v81"></a>SSMA v8.1

La versión v8.1 de SSMA para DB2 se ha mejorado para proporcionar correcciones de destino que están diseñadas para mejorar las métricas de calidad y la conversión.

> [!NOTE]
> Un problema conocido con la actualización automática puede producir el error de una actualización desde SSMA v8.0 a v8.1. Si se produce este error, descargue la nueva versión e instalarlo manualmente.

## <a name="ssma-v80"></a>SSMA v8.0

La versión v8.0 de SSMA para DB2 se ha mejorado para proporcionar diseñadas para mejorar la calidad y la conversión de las métricas de correcciones de destino. Esta versión también ofrece las siguientes características nuevas:

* Compatibilidad con **Azure SQL Database Managed Instance** como destino. Ahora puede crear nuevos proyectos destinados a la instancia administrada de Azure SQL Database:

  ![Proyecto de base de datos de SQL para MI](../media/ssma-newproject-sqldbmi.png)

* Después de la conversión **corrección advisor**. Más información sobre él [aquí](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/).

* Selección de base de datos/esquema preliminar.

  Al conectarse al origen, el usuario ahora puede seleccionar las bases de datos y esquemas de interés. Seleccionar sólo los esquemas que se va a migrar ahorrará tiempo durante la conexión inicial y mejorar el rendimiento general de SSMA.

  ![Objetos de filtro SSMA](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v7.10

La versión v7.10 de SSMA para DB2 contiene los siguientes cambios:

* Diseñado para proporcionar seguridad adicional y protecciones de seguridad para satisfacer los cambios en los requisitos globales correcciones de destino.
* Corrección de conversión de los bloques BEGIN-END.

## <a name="ssma-v79"></a>SSMA v7.9

La versión v7.9 de SSMA para DB2 contiene los siguientes cambios:

* Correcciones de destino que mejoran las métricas de calidad y la conversión.
* Soporte técnico en línea de comandos SSMA para modificar la asignación de tipos de datos y las preferencias del proyecto.
* Soporte técnico para migrar datos mediante SQL Server Integration Services (SSIS). Después de convertir el esquema, es posible crear un paquete SSIS mediante una opción del menú contextual.
* El cuadro de diálogo de conexión de Azure SQL Database de SSMA también se ha modificado para especificar el nombre completo del servidor. En versiones anteriores de SSMA, el prefijo de la base de datos de SQL Azure se tenía que se menciona explícitamente dentro de la configuración de proyectos.

## <a name="ssma-v78"></a>SSMA v7.8

La versión v7.8 de SSMA para DB2 contiene los siguientes cambios:

* Cambiar la asignación de tipos de resaltado en la configuración del proyecto.
* La capacidad de los usuarios deshabilitar la telemetría.

## <a name="ssma-v77"></a>SSMA v7.7

La versión v7.7 de SSMA para DB2 contiene los siguientes cambios:

* Correcciones de destino que mejoran las métricas de calidad y la conversión.
* Según la demanda popular, la versión de 32 bits de SSMA para DB2 es volver. En comparación con la implementación anterior (anterior a v7.4), hay dos paquetes de instalador, pero no se puede instalar en paralelo. Como resultado, debe elegir la versión más adecuada en función de los componentes de conectividad que tiene. Siempre es preferible usar la versión de 64 bits, si es posible.

## <a name="ssma-v76"></a>SSMA v7.6

La versión v7.6 de SSMA para DB2 se ha mejorado con correcciones de destino que mejoran la calidad y la conversión de las métricas y con compatibilidad con SQL Server 2017 (versión preliminar pública). Compatibilidad con SQL Server 2017 en Windows y Linux en versión preliminar pública y no debe usarse para las migraciones de producción.

## <a name="ssma-v75"></a>SSMA v7.5

La versión 7.5 de SSMA para DB2 se ha mejorado con varias mejoras para garantizar mayor accesibilidad para personas con discapacidades.

## <a name="ssma-v74"></a>SSMA v7.4

La versión v7.4 de SSMA para DB2 contiene los siguientes cambios:

* El **tiempo de espera de consulta** opción ahora está disponible durante la detección de objetos de esquema de origen y destino.

  ![opción de tiempo de espera de consulta](../media/query-timeout_red.png)

* La métrica de calidad y la conversión se ha mejorado con correcciones de destino, según los comentarios recibidos.

  > [!IMPORTANT]
  > .NET 4.5.2 es un requisito previo para la instalación de SSMA v7.4. Además, a partir de v7.4, la versión de 32 bits de SSMA se ha suspendido.

## <a name="ssma-v73"></a>SSMA v7.3

La versión v7.3 de SSMA para DB2 contiene los siguientes cambios:

* Métrica de calidad y la conversión mejorada con correcciones de destino según los comentarios recibidos.
* Marco de extensibilidad SSMA expuesta a través de los siguientes elementos:
  * Funcionalidad de exportación a un proyecto de SQL Server Data Tools (SSDT).
    * Ahora puede exportar las secuencias de comandos de esquema de SSMA para un proyecto de SSDT. Puede usar los scripts de esquema para realizar cambios de esquema adicional e implementar la base de datos.

      ![Guardar como comando de proyecto SSDT](../media/export-schema-scripts_red.png)
  * Bibliotecas que pueden utilizarse en SSMA para realizar conversiones personalizadas.
    * Ahora se puede crear código que pueda controlar las conversiones de sintaxis personalizada y las conversiones que antes no estaban controlaba SSMA.
      * Las instrucciones sobre cómo construir un convertidor personalizado están disponibles en esta entrada de blog, [funciones de conversión de ampliación de SQL Server Migration Assistant](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/).
      * Descargar un proyecto de ejemplo para la conversión de esta [entrada de blog](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/).

## <a name="ssma-v72"></a>SSMA v7.2

La versión v7.2 de SSMA para DB2 contiene los siguientes cambios:

* Métrica de calidad y la conversión mejorada con correcciones de destino según los comentarios recibidos.
* Mejoras de telemetría para proporcionar una mejor puntos de datos para solucionar problemas de los clientes y mejorar las tasas de conversión de SSMA.

## <a name="ssma-v71"></a>SSMA v7.1

La versión 7.1 de SSMA para DB2 contiene los siguientes cambios:

* SQL Server 2017 en Windows y Linux CTP1 ahora es una plataforma de destino admitida para la migración. Esta característica está en versión preliminar técnica y permite el movimiento de datos y esquema para servidores SQL Server de destino.
* Compatibilidad con las actualizaciones automáticas descargar la versión más reciente de SSMA en cuanto está disponible.
* Archivos binarios de instalación de SSMA ahora se entregan a través de los archivos de paquete de Windows installer (.msi).

## <a name="may-2016"></a>Mayo de 2016

La versión de mayo de 2016 de SSMA para DB2 contiene los siguientes cambios:  

* Se agregó compatibilidad para SQL Server 2016.
* Se ha agregado conversión de tablas en memoria y regulares de DB2 a las características de hekaton y en memoria de SQL Server.
* Se ha agregado conversión DB2 de controles de acceso a objetos de directiva de SQL Server (seguridad de nivel de fila para DB2).
* Se ha agregado conversión de tablas con versiones de sistema DB2 a las tablas temporales de SQL Server.
* Mejora en el analizador de DB2 y resolución.
* Quitar la comprobación de instalador para .net 2.0.
* Quitar *.dll innecesarios de instalador de Db2.
* Se ha corregido "guardar el proyecto" y "open project" comandos para la consola SSMA.
* Se ha corregido el comando "securepassword" para la consola SSMA.
* Se ha corregido el recuento de objetos para la carga inicial.
* Se corrigió el error en la configuración global.
  
## <a name="march-2016"></a>Marzo de 2016

La versión de vista previa de marzo de 2016 de SSMA para DB2 agrega compatibilidad para la migración a SQL Server 2016.

## <a name="january-2016"></a>Enero de 2016

La versión de mantenimiento de enero de 2016 de SSMA para DB2 contiene los siguientes cambios:  
  
* Se agregó compatibilidad para una serie de funciones estándares.  
* Se ha corregido errores del analizador de DB2.  
* Fijo DB2 v9 zOS soporte técnico (RFC 5690920).  
* DB2 fijo sin resolver errores de identificador durante la conversión.  
* La vista se ha agregado el elemento de menú de registro para SSMA (RFC 5706203).  
* Se ha agregado telemetría.
  
## <a name="november-2014"></a>Noviembre de 2014

La versión de noviembre de 2014 de SSMA para DB2 fue la versión inicial.
