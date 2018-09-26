---
title: Novedades de SSMA para DB2 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 09/22/2018
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 1cc38f85-3caa-42d0-8c76-a380c1d15c67
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 81a343c0ac4f37f02b0c461209a023f908ab608b
ms.sourcegitcommit: 7076fcb854c033a5dbeac7fcb22c5e15cf8528fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/19/2018
ms.locfileid: "46361999"
---
# <a name="whats-new-in-ssma-for-db2-db2tosql"></a>Novedades de SSMA para DB2 (DB2ToSQL)
En este artículo se enumera SSMA para DB2 cambios en cada versión.  

## <a name="ssma-v710"></a>SSMA v7.10
La versión v7.10 de SSMA para DB2 contiene los siguientes cambios:
- Diseñado para proporcionar seguridad adicional y protecciones de seguridad para satisfacer los cambios en los requisitos globales correcciones de destino.
- Corrección de conversión de los bloques BEGIN-END.

> [!IMPORTANT]
> Con SSMA v7.4 y versiones posteriores, .net 4.5.2 es un requisito previo de instalación.

## <a name="ssma-v79"></a>SSMA v7.9
La versión v7.9 de SSMA para DB2 contiene los siguientes cambios:
- Correcciones de destino que mejoran las métricas de calidad y la conversión.
- Soporte técnico en línea de comandos SSMA para modificar la asignación de tipos de datos y las preferencias del proyecto.
- Soporte técnico para migrar datos mediante SQL Server Integration Services (SSIS). Después de convertir el esquema, es posible crear un paquete SSIS mediante una opción del menú contextual.
- El cuadro de diálogo de conexión de Azure SQL Database de SSMA también se ha modificado para especificar el nombre completo del servidor. En versiones anteriores de SSMA, el prefijo de la base de datos de SQL Azure se tenía que se menciona explícitamente dentro de la configuración de proyectos.

> [!IMPORTANT]
> Con SSMA v7.4 y versiones posteriores, .net 4.5.2 es un requisito previo de instalación.

## <a name="ssma-v78"></a>SSMA v7.8
La versión v7.8 de SSMA para DB2 contiene los siguientes cambios:
- Asignación de tipo de cambio resaltado en la configuración del proyecto.
- Proporciona la capacidad de los usuarios deshabilitar la telemetría.

> [!IMPORTANT]
> Con SSMA v7.4 y versiones posteriores, .net 4.5.2 es un requisito previo de instalación.

## <a name="ssma-v77"></a>SSMA v7.7
La versión v7.7 de SSMA para DB2 contiene los siguientes cambios:
- SSMA para DB2 se ha mejorado con correcciones de destino que mejoran las métricas de calidad y la conversión.
- Según la demanda popular, la versión de 32 bits de SSMA para DB2 es volver. En comparación con la implementación anterior (anterior a v7.4), hay dos paquetes de instalador, pero no se puede instalar en paralelo. Como resultado, debe elegir la versión más adecuada en función de los componentes de conectividad que tiene. Siempre es preferible usar la versión de 64 bits, si es posible.

> [!IMPORTANT]
> Con SSMA v7.4 y versiones posteriores, .net 4.5.2 es un requisito previo de instalación.

## <a name="ssma-v76"></a>SSMA v7.6
Se ha mejorado la versión v7.6 de SSMA para DB2 con correcciones de destino que mejoran la calidad y la conversión de las métricas y con compatibilidad con SQL Server 2017 (versión preliminar pública). Compatibilidad con SQL Server 2017 en Windows y Linux en versión preliminar pública y no debe usarse para las migraciones de producción.

> [!IMPORTANT]
> Con SSMA v7.4 y versiones posteriores, .net 4.5.2 es un requisito previo de instalación y se ha dejado de usar la versión de 32 bits de la herramienta.

## <a name="ssma-v75"></a>SSMA v7.5
La versión 7.5 de SSMA para DB2 se ha mejorado con varias mejoras para garantizar mayor accesibilidad para personas con discapacidades.

> [!IMPORTANT]
> .NET 4.5.2 es un requisito previo para la instalación de SSMA v7.5. Además, a partir de v7.4, la versión de 32 bits de SSMA está en desuso.

## <a name="ssma-v74"></a>SSMA v7.4
La versión v7.4 de SSMA para DB2 contiene los siguientes cambios:
- El **tiempo de espera de consulta** opción ahora está disponible durante la detección de objetos de esquema de origen y destino.
![opción de tiempo de espera de consulta](../media/query-timeout_red.png)

- La métrica de calidad y la conversión se ha mejorado con correcciones de destino, según los comentarios recibidos.

> [!IMPORTANT]
> .NET 4.5.2 es un requisito previo para la instalación de SSMA v7.4. Además, a partir de v7.4, la versión de 32 bits de SSMA está en desuso.

## <a name="ssma-v73"></a>SSMA v7.3
La versión v7.3 de SSMA para DB2 contiene los siguientes cambios:
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
La versión v7.2 de SSMA para DB2 contiene los siguientes cambios:
- Métrica de calidad y la conversión mejorada con correcciones de destino según los comentarios recibidos.
- Mejoras de telemetría para proporcionar una mejor puntos de datos para solucionar problemas de los clientes y mejorar las tasas de conversión de SSMA.

## <a name="ssma-v71"></a>SSMA v7.1
La versión 7.1 de SSMA para Access contiene los siguientes cambios:
- SQL Server 2017 en Windows y Linux CTP1 ahora es una plataforma de destino admitida para la migración. Esta característica está en versión preliminar técnica y permite el movimiento de datos y esquema para servidores SQL Server de destino.
- SSMA ahora es compatible con las actualizaciones automáticas para descargar la versión más reciente de SSMA en cuanto está disponible.
- Archivos binarios de instalación de SSMA ahora se entregan a través de los archivos de paquete de Windows installer (.msi).

**Recursos**

[Funciones de conversión de SQL Server Migration Assistant de ampliación](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)

[Evaluar y migrar datos desde las plataformas de datos que no sea Microsoft SQL Server *(con el ejemplo de Oracle)*](https://blogs.msdn.microsoft.com/datamigration/2016/11/16/sql-server-migration-assistant-how-to-assess-and-migrate-databases-from-non-microsoft-data-platforms-to-sql-server/) 

## <a name="may-2016"></a>Mayo de 2016  
La versión de mayo de 2016 de SSMA para DB2 contiene los siguientes cambios:  

-  Se agregó compatibilidad para SQL Server 2016.
-  Se ha agregado conversión de tablas en memoria y regulares de DB2 a las características de hekaton y en memoria de SQL Server.
-  Se ha agregado conversión DB2 de controles de acceso a objetos de directiva de SQL Server (seguridad de nivel de fila para DB2).
-  Se ha agregado conversión de tablas con versiones de sistema DB2 a las tablas temporales de SQL Server.
-  Mejora en el analizador de DB2 y resolución.
-  Quitar la comprobación de instalador para .net 2.0.
-  Quitar *.dll innecesarios de instalador de Db2.
-  Se ha corregido "guardar el proyecto" y "open project" comandos para la consola SSMA.
-  Se ha corregido el comando "securepassword" para la consola SSMA.
-  Se ha corregido el recuento de objetos para la carga inicial.
-  Se corrigió el error en la configuración global.
  
## <a name="march-2016"></a>Marzo de 2016  
La versión de vista previa de marzo de 2016 de SSMA para DB2 contiene los siguientes cambios:  
  
-  Se agregó compatibilidad para la migración a SQL Server 2016.  
  
## <a name="january-2016"></a>Enero de 2016  
La versión de mantenimiento de enero de 2016 de SSMA para DB2 contiene los siguientes cambios:  
  
-  Se agregó compatibilidad para una serie de funciones estándares.  
-  Se ha corregido errores del analizador de DB2.  
-  Fijo DB2 v9 zOS soporte técnico (RFC 5690920).  
-  DB2 fijo sin resolver errores de identificador durante la conversión.  
-  La vista se ha agregado el elemento de menú de registro para SSMA (RFC 5706203).  
-  Se ha agregado telemetría.
  
## <a name="november-2014"></a>Noviembre de 2014  
La versión de noviembre de 2014 de SSMA para DB2 fue la versión inicial.
