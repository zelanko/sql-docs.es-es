---
title: "Configuración (cargar objetos) del proyecto (AccessToSQL) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 9ec1c1e8-a3e1-4e81-bf49-631f87daa209
caps.latest.revision: 4
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 84737c6b747174f993765a6d86081759cfedd4bb
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="project-settings-loading-objects-accesstosql"></a>Configuración (cargar objetos) del proyecto (AccessToSQL)
La configuración del proyecto cargar objetos permite configurar cómo se sincronizan los objetos de base de datos de Access con objetos de base de datos de SQL Server.  
  
Las acciones predeterminadas de especifican la configuración predeterminada para actualizar los objetos de la base de datos de Access y para sincronizar objetos con la base de datos de SQL Server. Para obtener más información, vea [actualizar desde la base de datos &#40; AccessToSQL &#41;](../../ssma/access/refresh-from-database-accesstosql.md)  
  
Puede tener acceso a dos páginas diferentes de sincronización que contengan los mismos valores:  
  
-   Para especificar la configuración para todos los proyectos futuros de SSMA, en la **herramientas** menú, haga clic en **DefaultProject configuración**y, a continuación, haga clic en **cargar objetos** en la parte inferior del panel izquierdo.  
  
-   Para especificar la configuración para el proyecto actual, en la **herramientas** menú, haga clic en **configuración del proyecto**y, a continuación, haga clic en **cargar objetos** en la parte inferior del panel izquierdo.  
  
## <a name="options"></a>Opciones  
  
##### <a name="misc"></a>Varios  
  
##### <a name="attempts"></a>Intentos  
Proporciona la información sobre el número de pases objetos llevar a cabo para cargar en SQL Server. Cargar objetos en SQL Server se suele realizar en varias fases. Objetos que no se pudo cargar en el primer paso, como las claves externas, pueden cargar correctamente en el siguiente paso.  
  
De forma predeterminada el valor es 2.  
  
## <a name="synchronization-for-sql-server"></a>Sincronización para SQL Server  
  
##### <a name="default-action-on-local-and-remote-object-change"></a>Acción predeterminada de cambio de objeto Local y remota  
Especifica la configuración predeterminada en el cuadro de diálogo de sincronización cuando la definición del objeto cambia de SSMA y en el servidor de base de datos.  
  
-   Si selecciona **actualizar desde la base de datos**, SSMA cargará las definiciones de base de datos en los metadatos cuando se cumple la condición.  
  
-   Si selecciona **escribir en la base de datos**, SSMA actualizará los objetos de la base de datos según el contenido de los metadatos SSMA cuando se cumpla la condición.  
  
-   Si selecciona **omitir**, SSMA no llevará a cabo las acciones de actualización.  
  
##### <a name="default-action-on-local-object-change"></a>Acción predeterminada de cambio de objeto local  
Especifica la configuración predeterminada en el cuadro de diálogo de sincronización cuando el objeto cambia de SSMA.  
  
-   Si selecciona **actualizar desde la base de datos**, SSMA cargará las definiciones de base de datos en los metadatos cuando se cumple la condición.  
  
-   Si selecciona **escribir en la base de datos**, SSMA actualizará el objeto en la base de datos según el contenido de los metadatos SSMA cuando se cumple la condición.  
  
-   Si selecciona **omitir**, SSMA no llevará a cabo las acciones de actualización.  
  
##### <a name="default-action-on-remote-object-change"></a>Acción predeterminada de cambio de objeto remoto  
Especifica la configuración predeterminada en el cuadro de diálogo de sincronización cuando cambian los objetos en el servidor de base de datos.  
  
-   Si selecciona **actualizar desde la base de datos**, SSMA cargará las definiciones de base de datos en los metadatos cuando se cumple la condición.  
  
-   Si selecciona **escribir en la base de datos**, SSMA actualizará el objeto en la base de datos según el contenido de los metadatos SSMA cuando se cumple la condición.  
  
-   Si selecciona **omitir**, SSMA no llevará a cabo las acciones de actualización.  
  
##### <a name="default-action-when-local-object-metadata-is-missing"></a>Acción de predeterminada una vez que faltan metadatos del objeto local  
Especifica la configuración predeterminada en el cuadro de diálogo sincronización una vez que faltan los metadatos locales.  
  
-   Si selecciona **actualizar desde la base de datos**, SSMA selecciona la actualización de la opción de base de datos cuando se cumple la condición.  
  
-   Si selecciona **escribir en la base de datos**, SSMA eliminará el objeto de la base de datos cuando se cumpla la condición.  
  
-   Si selecciona **omitir**, SSMA no llevará a cabo las acciones de actualización.  
  

