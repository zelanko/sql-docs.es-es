---
title: Configuración (sincronización) (MySQLToSQL) del proyecto | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 42061ff7-e6e7-497b-a0d9-440b9cf5986c
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: c4437f76a926e84ffe3592042f9d29b50f3eabf9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67908842"
---
# <a name="project-settings-synchronization-mysqltosql"></a>Configuración del proyecto (sincronización) (MySQLToSQL)
La sincronización **configuración del proyecto** le permiten configurar cómo se sincronizan los objetos de base de datos de MySQL con objetos de base de datos de SQL Server.  
  
Las acciones predeterminadas de especifican la configuración predeterminada para actualizar objetos de la base de datos MySQL y para la sincronización de objetos con la base de datos de SQL Server. Para obtener más información, consulte [actualizar desde la base de datos &#40;MySQLToSQL&#41;](../../ssma/mysql/refresh-from-database-mysqltosql.md)  
  
Puede tener acceso a dos páginas diferentes de sincronización que contienen los mismos valores:  
  
-   Para especificar la configuración para todos los proyectos SSMA futuros, en el **herramientas** menú, haga clic en **DefaultProject configuración**y, a continuación, haga clic en **sincronización** en la parte inferior del panel izquierdo.  
  
-   Para especificar la configuración para el proyecto actual, en el **herramientas** menú, haga clic en **configuración del proyecto**y, a continuación, haga clic en **sincronización** en la parte inferior del panel izquierdo.  
  
## <a name="options"></a>Opciones  
  
##### <a name="misc"></a>Varios  
  
##### <a name="attempts"></a>Intentos  
Proporciona la información sobre el número de pasadas de objetos seguir para cargar en SQL Server. Cargando objetos en SQL Server se suele realizar en varias fases. Objetos que no se pueden cargar en la primera pasada, como las claves externas, es posible que cargarán correctamente en el siguiente paso.  
  
De forma predeterminada el valor es 2.  
  
## <a name="synchronization-for-mysql"></a>Sincronización de MySQL  
  
##### <a name="action-on-local-and-remote-object-change"></a>Acción de cambio de los objetos locales y remotos  
Especifica la configuración predeterminada en el cuadro de diálogo de sincronización cuando la definición del objeto cambia de SSMA y en el servidor de base de datos.  
  
-   Si selecciona la actualización de base de datos, SSMA cargará las definiciones de base de datos en los metadatos cuando se cumple la condición.  
  
-   Si selecciona Omitir, SSMA no realizará ninguna acción de actualización.  
  
##### <a name="action-on-local-object-change"></a>Acción de cambio de objeto local  
Especifica la configuración predeterminada en el cuadro de diálogo de sincronización cuando cambia el objeto en SSMA.  
  
-   Si selecciona **actualizar desde la base de datos**, SSMA cargará las definiciones de base de datos en los metadatos cuando se cumple la condición.  
  
-   Si selecciona **Skip**, SSMA no realizará ninguna acción de actualización.  
  
##### <a name="action-on-remote-object-change"></a>Acción de cambio de objeto remoto  
Especifica la configuración predeterminada en el cuadro de diálogo de sincronización cuando cambian los objetos en el servidor de base de datos.  
  
-   Si selecciona **actualizar desde la base de datos**, SSMA cargará las definiciones de base de datos en los metadatos cuando se cumple la condición.  
  
-   Si selecciona **Skip**, SSMA no realizará ninguna acción de actualización.  
  
##### <a name="action-when-local-object-metadata-is-missing"></a>Acción cuando faltan los metadatos del objeto local  
Especifica la configuración predeterminada en el cuadro de diálogo de sincronización cuando faltan los metadatos locales.  
  
-   Si selecciona **actualizar desde la base de datos**, SSMA cargará las definiciones de base de datos en los metadatos cuando se cumple la condición.  
  
-   Si selecciona **Skip**, SSMA no realizará ninguna acción de actualización  
  
## <a name="synchronization-for-sql-server"></a>Sincronización de SQL Server  
  
##### <a name="action-on-local-and-remote-object-change"></a>Acción de cambio de objeto Local y remota  
Especifica la configuración predeterminada en el cuadro de diálogo de sincronización cuando la definición del objeto cambia de SSMA y en el servidor de base de datos.  
  
-   Si selecciona **actualizar desde la base de datos**, SSMA cargará las definiciones de base de datos en los metadatos cuando se cumple la condición.  
  
-   Si selecciona **escribir en la base de datos**, SSMA actualizará los objetos de la base de datos según el contenido de los metadatos SSMA cuando se cumple la condición.  
  
-   Si selecciona **Skip**, SSMA no realizará ninguna acción de actualización.  
  
##### <a name="action-on-local-object-change"></a>Acción de cambio de objeto local  
Especifica la configuración predeterminada en el cuadro de diálogo de sincronización cuando cambia el objeto en SSMA.  
  
-   Si selecciona **actualizar desde la base de datos**, SSMA cargará las definiciones de base de datos en los metadatos cuando se cumple la condición.  
  
-   Si selecciona **escribir en la base de datos**, SSMA actualizará el objeto en la base de datos según el contenido de los metadatos SSMA cuando se cumple la condición.  
  
-   Si selecciona **Skip**, SSMA no realizará ninguna acción de actualización.  
  
##### <a name="action-on-remote-object-change"></a>Acción de cambio de objeto remoto  
Especifica la configuración predeterminada en el cuadro de diálogo de sincronización cuando cambian los objetos en el servidor de base de datos.  
  
-   Si selecciona **actualizar desde la base de datos**, SSMA cargará las definiciones de base de datos en los metadatos cuando se cumple la condición.  
  
-   Si selecciona **escribir en la base de datos**, SSMA actualizará el objeto en la base de datos según el contenido de los metadatos SSMA cuando se cumple la condición.  
  
-   Si selecciona **Skip**, SSMA no realizará ninguna acción de actualización.  
  
##### <a name="action-when-local-object-metadata-is-missing"></a>Acción cuando faltan los metadatos del objeto local  
Especifica la configuración predeterminada en el cuadro de diálogo de sincronización cuando faltan los metadatos locales.  
  
-   Si selecciona **actualizar desde la base de datos**, SSMA selecciona la actualización de la opción de base de datos cuando se cumple la condición.  
  
-   Si selecciona **escribir en la base de datos**, SSMA eliminará el objeto de la base de datos cuando se cumple la condición.  
  
-   Si selecciona **Skip**, SSMA no realizará ninguna acción de actualización.  
  
