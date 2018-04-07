---
title: Proyecto Settings(Synchronization) (DB2ToSQL) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-db2
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: a5629a72-8c17-46a4-bb4d-19d51a0b98a2
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: da4be629e37646b10011c76f5a78a2cde246865e
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="project-settingssynchronization-db2tosql"></a>Proyecto Settings(Synchronization) (DB2ToSQL)
La página de sincronización de la **configuración del proyecto** cuadro de diálogo contiene opciones que personalizan la carga de SSMA y las actualizaciones de base de datos de objetos, como tablas y procedimientos almacenados, en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
Las opciones de acciones predeterminadas especifican valores predeterminados para actualizar los objetos de la base de datos de DB2 y para sincronizar objetos con la base de datos de SQL Server. Para obtener más información, consulte [actualizar desde la base de datos &#40;DB2ToSQL&#41;](../../ssma/db2/refresh-from-database-db2tosql.md).  
  
Puede tener acceso a dos páginas diferentes de sincronización que contengan los mismos valores:  
  
-   Para especificar la configuración para todos los proyectos futuros de SSMA, en la **herramientas** menú, haga clic en **la configuración predeterminada del proyecto**y, a continuación, haga clic en **sincronización** en la parte inferior del panel izquierdo.  
  
-   Para especificar la configuración para el proyecto actual, en la **herramientas** menú, haga clic en **configuración del proyecto**y, a continuación, haga clic en **sincronización** en la parte inferior del panel izquierdo.  
  
## <a name="miscellaneous-options"></a>Otras opciones  
**Intentos**  
Especifica el número de intentos de SSMA debe realizar cuando carga los objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Objetos que no se cargan en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] en el intento actual se intentará de nuevo hasta que SSMA alcanza el número máximo de intentos en el proceso de sincronización actual. Establecido un valor predeterminado es **2**  
  
## <a name="synchronization-for-db2-options"></a>Sincronización de las opciones de DB2  
**Acción de cambio de objetos locales y remotos**  
Especifica la configuración predeterminada en el cuadro de diálogo de sincronización cuando la definición del objeto cambia de SSMA y en el servidor de base de datos. Establecido un valor predeterminado es **actualizar desde la base de datos**.  
  
-   Si selecciona **actualizar desde la base de datos**, SSMA cargará las definiciones de base de datos en los metadatos cuando se cumple la condición.  
  
-   Si selecciona **omitir**, SSMA no llevará a cabo las acciones de actualización.  
  
**Acción de cambio de objeto local**  
Especifica la configuración predeterminada en el cuadro de diálogo de sincronización cuando el objeto cambia de SSMA. Establecido un valor predeterminado es **omitir**.  
  
-   Si selecciona **actualizar desde la base de datos**, SSMA cargará las definiciones de base de datos en los metadatos cuando se cumple la condición.  
  
-   Si selecciona **omitir**, SSMA no llevará a cabo las acciones de actualización.  
  
**Acción de cambio de objeto remoto**  
Especifica la configuración predeterminada en el cuadro de diálogo de sincronización cuando cambian los objetos en el servidor de base de datos. Establecido un valor predeterminado es **actualizar desde la base de datos**.  
  
-   Si selecciona **actualizar desde la base de datos**, SSMA cargará las definiciones de base de datos en los metadatos cuando se cumple la condición.  
  
-   Si selecciona **omitir**, SSMA no llevará a cabo las acciones de actualización.  
  
**Acción una vez que faltan metadatos del objeto local**  
Especifica la configuración predeterminada en el cuadro de diálogo sincronización una vez que faltan los metadatos locales. Establecido un valor predeterminado es **actualizar desde la base de datos**.  
  
-   Si selecciona **actualizar desde la base de datos**, SSMA SSMA cargará las definiciones de base de datos en los metadatos cuando se cumple la condición.  
  
-   Si selecciona **omitir**, SSMA no llevará a cabo las acciones de actualización.  
  
## <a name="synchronization-for-sql-server-options"></a>Sincronización de las opciones de SQL Server  
**Acción de cambio de objetos locales y remotos**  
Especifica la configuración predeterminada en el cuadro de diálogo de sincronización cuando la definición del objeto cambia de SSMA y en el servidor de base de datos. Establecido un valor predeterminado es **escritura a la base de datos**.  
  
-   Si selecciona **actualizar desde la base de datos**, SSMA cargará las definiciones de base de datos en los metadatos cuando se cumple la condición.  
  
-   Si selecciona **escribir en la base de datos**, SSMA actualizará los objetos de la base de datos según el contenido de los metadatos SSMA cuando se cumpla la condición.  
  
-   Si selecciona **omitir**, SSMA no llevará a cabo las acciones de actualización.  
  
**Acción de cambio de objeto local**  
Especifica la configuración predeterminada en el cuadro de diálogo de sincronización cuando el objeto cambia de SSMA. Establecido un valor predeterminado es **escritura a la base de datos**.  
  
-   Si selecciona **actualizar desde la base de datos**, SSMA cargará las definiciones de base de datos en los metadatos cuando se cumple la condición.  
  
-   Si selecciona **escribir en la base de datos**, SSMA actualizará el objeto en la base de datos según el contenido de los metadatos SSMA cuando se cumple la condición.  
  
-   Si selecciona **omitir**, SSMA no llevará a cabo las acciones de actualización.  
  
**Acción de cambio de objeto remoto**  
Especifica la configuración predeterminada en el cuadro de diálogo de sincronización cuando cambian los objetos en el servidor de base de datos.  Establecido un valor predeterminado es **actualizar desde la base de datos**.  
  
-   Si selecciona **actualizar desde la base de datos**, SSMA cargará las definiciones de base de datos en los metadatos cuando se cumple la condición.  
  
-   Si selecciona **escribir en la base de datos**, SSMA actualizará el objeto en la base de datos según el contenido de los metadatos SSMA cuando se cumple la condición.  
  
-   Si selecciona **omitir**, SSMA no llevará a cabo las acciones de actualización.  
  
**Acción una vez que faltan metadatos del objeto local**  
Especifica la configuración predeterminada en el cuadro de diálogo sincronización una vez que faltan los metadatos locales. Establecido un valor predeterminado es **actualizar desde la base de datos**.  
  
-   Si selecciona **actualizar desde la base de datos**, SSMA selecciona el **actualizar desde la base de datos** cuando se cumple la condición.  
  
-   Si selecciona **escribir en la base de datos**, SSMA eliminará el objeto de la base de datos cuando se cumpla la condición.  
  
-   Si selecciona **omitir**, SSMA no llevará a cabo las acciones de actualización.  
  
