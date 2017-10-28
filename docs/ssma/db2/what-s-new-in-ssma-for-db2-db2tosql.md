---
title: "¿Qué &#39; s de SSMA para DB2 (DB2ToSQL) | Documentos de Microsoft"
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
ms.assetid: 1cc38f85-3caa-42d0-8c76-a380c1d15c67
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: e3c781449a8f7a1b236508cd21b8c00ff175774f
ms.openlocfilehash: 8246a40f5fd59ae4d8a28f1e0315ea1a015e8e7d
ms.contentlocale: es-es
ms.lasthandoff: 09/30/2017

---
# <a name="what39s-new-in-ssma-for-db2-db2tosql"></a>¿Qué &#39; s de SSMA para DB2 (DB2ToSQL)
Este tema enumeran SSMA para cambios de DB2 en cada versión.  

## <a name="ssma-v76"></a>SSMA v7.6
Se ha mejorado la versión v7.6 de SSMA para DB2 con correcciones de destino que mejoran las métricas de calidad y la conversión y con el soporte para SQL Server 2017 (vista previa pública). Compatibilidad con SQL Server 2017 en Windows y Linux se encuentra en versión preliminar pública y no debe usarse para las migraciones de producción.

> [!IMPORTANT]
> Con SSMA v7.4 y versiones posteriores, .net 4.5.2 es un requisito previo de instalación y se ha cancelado la versión de 32 bits de la herramienta.

## <a name="ssma-v75"></a>SSMA 7.5
La versión 7.5 de SSMA para DB2 se ha mejorado con varias mejoras para garantizar una mayor accesibilidad para personas con discapacidades.

> [!IMPORTANT]
> .NET 4.5.2 es un requisito previo para la instalación de SSMA 7.5. Además, a partir de v7.4, la versión de 32 bits de SSMA se está suspendida.

## <a name="ssma-v74"></a>SSMA v7.4
La versión v7.4 de SSMA para DB2 contiene los siguientes cambios:
- El **tiempo de espera de consulta** opción ahora está disponible durante la detección de objetos de esquema en el origen y de destino.
![opción de tiempo de espera de consulta](../media/query-timeout_red.png)

- La métrica de calidad y la conversión se ha mejorado con correcciones de destino, en función de los comentarios de clientes.

> [!IMPORTANT]
> .NET 4.5.2 es un requisito previo para la instalación de SSMA v7.4. Además, a partir de v7.4, la versión de 32 bits de SSMA se está suspendida.

## <a name="ssma-v73"></a>SSMA v7.3
La versión v7.3 de SSMA para DB2 contiene los siguientes cambios:
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
La versión de v7.2 de SSMA para DB2 contiene los siguientes cambios:
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
La versión de mayo de 2016 de SSMA para DB2 contiene los siguientes cambios:  

-  Se agregó compatibilidad para SQL Server 2016.
-  Agregada la conversión de tablas de DB2 en memoria y regulares a las características de hekaton y en memoria de SQL Server.
-  Conversión agregada DB2 de controles de acceso a objetos de directiva de SQL Server (seguridad de nivel de fila para DB2).
-  Agregada la conversión de tablas de versiones del sistema DB2 en tablas temporales de SQL Server.
-  Mejora en el analizador de DB2 y resolución.
-  Quita la comprobación de instalador para .net 2.0.
-  Quita *.dll innecesarios del instalador de Db2.
-  Fija "guardar el proyecto" y "Abrir proyecto" comandos de consola SSMA.
-  Se ha corregido "securepassword" comando de consola SSMA.
-  Se ha corregido el recuento de objetos para la carga inicial.
-  Ha corregido el error en configuración global.
  
## <a name="march-2016"></a>Marzo de 2016  
La versión de vista previa de marzo de 2016 de SSMA para DB2 contiene los siguientes cambios:  
  
-  Se agregó compatibilidad para la migración a SQL Server 2016.  
  
## <a name="january-2016"></a>Enero de 2016  
La versión de mantenimiento de enero de 2016 de SSMA para DB2 contiene los siguientes cambios:  
  
-  Se agregó compatibilidad para una serie de funciones estándares.  
-  Se corrigieron errores del analizador de DB2.  
-  Fijo DB2 v9 zOS soporte (RFC 5690920).  
-  DB2 fijo sin resolver errores de identificador durante la conversión.  
-  Vista ha agregado el elemento de menú de registro para SSMA (RFC 5706203).  
-  Telemetría agregada.
  
## <a name="november-2014"></a>Noviembre de 2014  
La versión de noviembre de 2014 de SSMA para DB2 fue la versión inicial.

