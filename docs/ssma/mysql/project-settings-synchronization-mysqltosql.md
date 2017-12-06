---
title: "Configuración (sincronización) (MySQLToSQL) del proyecto | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-mysql
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 42061ff7-e6e7-497b-a0d9-440b9cf5986c
caps.latest.revision: "3"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8ff2ac36451187b0d74087043142969cde9560ee
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="project-settings-synchronization-mysqltosql"></a>Configuración del proyecto (la sincronización) (MySQLToSQL)
La sincronización **configuración del proyecto** le permiten configurar cómo se sincronizan los objetos de base de datos de MySQL con objetos de base de datos de SQL Server.  
  
Las acciones predeterminadas de especifican la configuración predeterminada para actualizar los objetos de la base de datos MySQL y para sincronizar objetos con la base de datos de SQL Server. Para obtener más información, vea [actualizar desde la base de datos &#40; MySQLToSQL &#41;](../../ssma/mysql/refresh-from-database-mysqltosql.md)  
  
Puede tener acceso a dos páginas diferentes de sincronización que contengan los mismos valores:  
  
-   Para especificar la configuración para todos los proyectos futuros de SSMA, en la **herramientas** menú, haga clic en **DefaultProject configuración**y, a continuación, haga clic en **sincronización** en la parte inferior del panel izquierdo.  
  
-   Para especificar la configuración para el proyecto actual, en la **herramientas** menú, haga clic en **configuración del proyecto**y, a continuación, haga clic en **sincronización** en la parte inferior del panel izquierdo.  
  
## <a name="options"></a>Opciones  
  
##### <a name="misc"></a>Varios  
  
##### <a name="attempts"></a>Intentos  
Proporciona la información sobre el número de pases objetos llevar a cabo para cargar en SQL Server. Cargar objetos en SQL Server se suele realizar en varias fases. Objetos que no se pudo cargar en el primer paso, como las claves externas, pueden cargar correctamente en el siguiente paso.  
  
De forma predeterminada el valor es 2.  
  
## <a name="synchronization-for-mysql"></a>Sincronización de MySQL  
  
##### <a name="action-on-local-and-remote-object-change"></a>Acción de cambio de objetos locales y remotos  
Especifica la configuración predeterminada en el cuadro de diálogo de sincronización cuando la definición del objeto cambia de SSMA y en el servidor de base de datos.  
  
-   Si selecciona la actualización de base de datos, SSMA cargar definiciones de base de datos en los metadatos cuando se cumpla la condición.  
  
-   Si selecciona Omitir, SSMA no realizará ninguna acción de actualización.  
  
##### <a name="action-on-local-object-change"></a>Acción de cambio de objeto local  
Especifica la configuración predeterminada en el cuadro de diálogo de sincronización cuando el objeto cambia de SSMA.  
  
-   Si selecciona **actualizar desde la base de datos**, SSMA cargará las definiciones de base de datos en los metadatos cuando se cumple la condición.  
  
-   Si selecciona **omitir**, SSMA no llevará a cabo las acciones de actualización.  
  
##### <a name="action-on-remote-object-change"></a>Acción de cambio de objeto remoto  
Especifica la configuración predeterminada en el cuadro de diálogo de sincronización cuando cambian los objetos en el servidor de base de datos.  
  
-   Si selecciona **actualizar desde la base de datos**, SSMA cargará las definiciones de base de datos en los metadatos cuando se cumple la condición.  
  
-   Si selecciona **omitir**, SSMA no llevará a cabo las acciones de actualización.  
  
##### <a name="action-when-local-object-metadata-is-missing"></a>Acción una vez que faltan metadatos del objeto local  
Especifica la configuración predeterminada en el cuadro de diálogo sincronización una vez que faltan los metadatos locales.  
  
-   Si selecciona **actualizar desde la base de datos**, SSMA SSMA cargará las definiciones de base de datos en los metadatos cuando se cumple la condición.  
  
-   Si selecciona **omitir**, SSMA no llevará a cabo las acciones de actualización  
  
## <a name="synchronization-for-sql-server"></a>Sincronización para SQL Server  
  
##### <a name="action-on-local-and-remote-object-change"></a>Acción de cambio de objeto Local y remota  
Especifica la configuración predeterminada en el cuadro de diálogo de sincronización cuando la definición del objeto cambia de SSMA y en el servidor de base de datos.  
  
-   Si selecciona **actualizar desde la base de datos**, SSMA cargará las definiciones de base de datos en los metadatos cuando se cumple la condición.  
  
-   Si selecciona **escribir en la base de datos**, SSMA actualizará los objetos de la base de datos según el contenido de los metadatos SSMA cuando se cumpla la condición.  
  
-   Si selecciona **omitir**, SSMA no llevará a cabo las acciones de actualización.  
  
##### <a name="action-on-local-object-change"></a>Acción de cambio de objeto local  
Especifica la configuración predeterminada en el cuadro de diálogo de sincronización cuando el objeto cambia de SSMA.  
  
-   Si selecciona **actualizar desde la base de datos**, SSMA cargará las definiciones de base de datos en los metadatos cuando se cumple la condición.  
  
-   Si selecciona **escribir en la base de datos**, SSMA actualizará el objeto en la base de datos según el contenido de los metadatos SSMA cuando se cumple la condición.  
  
-   Si selecciona **omitir**, SSMA no llevará a cabo las acciones de actualización.  
  
##### <a name="action-on-remote-object-change"></a>Acción de cambio de objeto remoto  
Especifica la configuración predeterminada en el cuadro de diálogo de sincronización cuando cambian los objetos en el servidor de base de datos.  
  
-   Si selecciona **actualizar desde la base de datos**, SSMA cargará las definiciones de base de datos en los metadatos cuando se cumple la condición.  
  
-   Si selecciona **escribir en la base de datos**, SSMA actualizará el objeto en la base de datos según el contenido de los metadatos SSMA cuando se cumple la condición.  
  
-   Si selecciona **omitir**, SSMA no llevará a cabo las acciones de actualización.  
  
##### <a name="action-when-local-object-metadata-is-missing"></a>Acción una vez que faltan metadatos del objeto local  
Especifica la configuración predeterminada en el cuadro de diálogo sincronización una vez que faltan los metadatos locales.  
  
-   Si selecciona **actualizar desde la base de datos**, SSMA selecciona la actualización de la opción de base de datos cuando se cumple la condición.  
  
-   Si selecciona **escribir en la base de datos**, SSMA eliminará el objeto de la base de datos cuando se cumpla la condición.  
  
-   Si selecciona **omitir**, SSMA no llevará a cabo las acciones de actualización.  
  
