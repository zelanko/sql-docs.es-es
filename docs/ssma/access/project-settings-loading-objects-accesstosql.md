---
title: (Carga de objetos) de configuración del proyecto (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9ec1c1e8-a3e1-4e81-bf49-631f87daa209
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 90a47a7586d0f3c6b5bd0fee28ed01f3b292a92e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63299454"
---
# <a name="project-settings-loading-objects-accesstosql"></a>(Carga de objetos) de configuración del proyecto (AccessToSQL)
La configuración del proyecto al cargar objetos permite configurar cómo obtener acceso a objetos de base de datos se sincronizan con objetos de base de datos de SQL Server.  
  
Las acciones predeterminadas de especifican la configuración predeterminada para actualizar objetos de la base de datos de Access y sincronización de objetos con la base de datos de SQL Server. Para obtener más información, consulte [actualizar desde la base de datos &#40;AccessToSQL&#41;](../../ssma/access/refresh-from-database-accesstosql.md)  
  
Puede tener acceso a dos páginas diferentes de sincronización que contienen los mismos valores:  
  
-   Para especificar la configuración para todos los proyectos SSMA futuros, en el **herramientas** menú, haga clic en **DefaultProject configuración**y, a continuación, haga clic en **cargar objetos** en la parte inferior del panel izquierdo.  
  
-   Para especificar la configuración para el proyecto actual, en el **herramientas** menú, haga clic en **configuración del proyecto**y, a continuación, haga clic en **cargar objetos** en la parte inferior del panel izquierdo.  
  
## <a name="options"></a>Opciones  
  
##### <a name="misc"></a>Varios  
  
##### <a name="attempts"></a>Intentos  
Proporciona la información sobre el número de pasadas de objetos seguir para cargar en SQL Server. Cargando objetos en SQL Server se suele realizar en varias fases. Objetos que no se pueden cargar en la primera pasada, como las claves externas, es posible que cargarán correctamente en el siguiente paso.  
  
De forma predeterminada el valor es 2.  
  
## <a name="synchronization-for-sql-server"></a>Sincronización de SQL Server  
  
##### <a name="default-action-on-local-and-remote-object-change"></a>Acción predeterminada en el cambio de objeto Local y remota  
Especifica la configuración predeterminada en el cuadro de diálogo de sincronización cuando la definición del objeto cambia de SSMA y en el servidor de base de datos.  
  
-   Si selecciona **actualizar desde la base de datos**, SSMA cargará las definiciones de base de datos en los metadatos cuando se cumple la condición.  
  
-   Si selecciona **escribir en la base de datos**, SSMA actualizará los objetos de la base de datos según el contenido de los metadatos SSMA cuando se cumple la condición.  
  
-   Si selecciona **Skip**, SSMA no realizará ninguna acción de actualización.  
  
##### <a name="default-action-on-local-object-change"></a>Acción predeterminada en el cambio de objeto local  
Especifica la configuración predeterminada en el cuadro de diálogo de sincronización cuando cambia el objeto en SSMA.  
  
-   Si selecciona **actualizar desde la base de datos**, SSMA cargará las definiciones de base de datos en los metadatos cuando se cumple la condición.  
  
-   Si selecciona **escribir en la base de datos**, SSMA actualizará el objeto en la base de datos según el contenido de los metadatos SSMA cuando se cumple la condición.  
  
-   Si selecciona **Skip**, SSMA no realizará ninguna acción de actualización.  
  
##### <a name="default-action-on-remote-object-change"></a>Acción predeterminada en el cambio de objeto remoto  
Especifica la configuración predeterminada en el cuadro de diálogo de sincronización cuando cambian los objetos en el servidor de base de datos.  
  
-   Si selecciona **actualizar desde la base de datos**, SSMA cargará las definiciones de base de datos en los metadatos cuando se cumple la condición.  
  
-   Si selecciona **escribir en la base de datos**, SSMA actualizará el objeto en la base de datos según el contenido de los metadatos SSMA cuando se cumple la condición.  
  
-   Si selecciona **Skip**, SSMA no realizará ninguna acción de actualización.  
  
##### <a name="default-action-when-local-object-metadata-is-missing"></a>Acción predeterminada cuando los metadatos del objeto local están que faltan  
Especifica la configuración predeterminada en el cuadro de diálogo de sincronización cuando faltan los metadatos locales.  
  
-   Si selecciona **actualizar desde la base de datos**, SSMA selecciona la actualización de la opción de base de datos cuando se cumple la condición.  
  
-   Si selecciona **escribir en la base de datos**, SSMA eliminará el objeto de la base de datos cuando se cumple la condición.  
  
-   Si selecciona **Skip**, SSMA no realizará ninguna acción de actualización.  
  
