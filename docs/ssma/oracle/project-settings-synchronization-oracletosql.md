---
title: Configuración del proyecto (sincronización) (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: e223fb7d-05ec-4fa5-8973-d845c33a23dd
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 743ed010107c9557c84b1683f7a81b369ca7cf3c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68266588"
---
# <a name="project-settingssynchronization-oracletosql"></a>Configuración del proyecto (sincronización) (OracleToSQL)
La página sincronización del cuadro de diálogo **configuración del proyecto** contiene opciones que personalizan el modo en que SSMA carga y actualiza los objetos de base de datos, como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tablas y procedimientos almacenados, en.  
  
Las opciones de acciones predeterminadas especifican la configuración predeterminada para actualizar objetos de la base de datos de Oracle y para sincronizar objetos con la base de datos de SQL Server. Para obtener más información, vea [actualizar desde base de datos: Oracle](../../ssma/oracle/refresh-from-database-oracletosql.md).  
  
Puede tener acceso a dos páginas de sincronización diferentes que contengan la misma configuración:  
  
-   Para especificar la configuración de todos los proyectos de SSMA futuros, en el menú **herramientas** , haga clic en **configuración predeterminada del proyecto**y, a continuación, haga clic en **sincronización** en la parte inferior del panel izquierdo.  
  
-   Para especificar la configuración del proyecto actual, en el menú **herramientas** , haga clic en **configuración del proyecto**y, a continuación, haga clic en **sincronización** en la parte inferior del panel izquierdo.  
  
## <a name="miscellaneous-options"></a>Otras opciones  
**Fallido**  
Especifica el número de intentos que SSMA debe realizar cuando carga objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los objetos que no se cargan en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el intento actual se intentarán de nuevo hasta que SSMA alcance el número máximo de intentos en el proceso de sincronización actual. El conjunto de valores predeterminado es **2**  
  
## <a name="synchronization-for-oracle-options"></a>Sincronización para opciones de Oracle  
**Acción en el cambio de objetos locales y remotos**  
Especifica el valor predeterminado en el cuadro de diálogo de sincronización cuando la definición del objeto cambia en SSMA y en el servidor de base de datos. El conjunto de valores predeterminado es **actualizar desde la base de datos**.  
  
-   Si selecciona **actualizar desde base de**datos, SSMA cargará las definiciones de base de datos en los metadatos cuando se cumpla la condición.  
  
-   Si selecciona **omitir**, SSMA no realizará ninguna acción de actualización.  
  
**Acción en el cambio de objeto local**  
Especifica el valor predeterminado en el cuadro de diálogo de sincronización cuando el objeto cambia en SSMA. El valor predeterminado establecido es **omitir**.  
  
-   Si selecciona **actualizar desde base de**datos, SSMA cargará las definiciones de base de datos en los metadatos cuando se cumpla la condición.  
  
-   Si selecciona **omitir**, SSMA no realizará ninguna acción de actualización.  
  
**Acción en el cambio de objeto remoto**  
Especifica el valor predeterminado en el cuadro de diálogo de sincronización cuando los objetos cambian en el servidor de base de datos. El conjunto de valores predeterminado es **actualizar desde la base de datos**.  
  
-   Si selecciona **actualizar desde base de**datos, SSMA cargará las definiciones de base de datos en los metadatos cuando se cumpla la condición.  
  
-   Si selecciona **omitir**, SSMA no realizará ninguna acción de actualización.  
  
**Acción cuando faltan metadatos de objeto local**  
Especifica el valor predeterminado en el cuadro de diálogo de sincronización cuando faltan metadatos locales. El conjunto de valores predeterminado es **actualizar desde la base de datos**.  
  
-   Si selecciona **actualizar desde base de**datos, SSMA cargará las definiciones de base de datos en los metadatos cuando se cumpla la condición.  
  
-   Si selecciona **omitir**, SSMA no realizará ninguna acción de actualización.  
  
## <a name="synchronization-for-sql-server-options"></a>Sincronización de opciones de SQL Server  
**Acción en el cambio de objetos locales y remotos**  
Especifica el valor predeterminado en el cuadro de diálogo de sincronización cuando la definición del objeto cambia en SSMA y en el servidor de base de datos. El valor predeterminado establecido es **escribir en la base de datos**.  
  
-   Si selecciona **actualizar desde base de**datos, SSMA cargará las definiciones de base de datos en los metadatos cuando se cumpla la condición.  
  
-   Si selecciona **escribir en la base**de datos, SSMA actualizará los objetos de la base de datos según el contenido de los metadatos de SSMA cuando se cumpla la condición.  
  
-   Si selecciona **omitir**, SSMA no realizará ninguna acción de actualización.  
  
**Acción en el cambio de objeto local**  
Especifica el valor predeterminado en el cuadro de diálogo de sincronización cuando el objeto cambia en SSMA. El valor predeterminado establecido es **escribir en la base de datos**.  
  
-   Si selecciona **actualizar desde base de**datos, SSMA cargará las definiciones de base de datos en los metadatos cuando se cumpla la condición.  
  
-   Si selecciona **escribir en la base**de datos, SSMA actualizará el objeto en la base de datos según el contenido de los metadatos de SSMA cuando se cumpla la condición.  
  
-   Si selecciona **omitir**, SSMA no realizará ninguna acción de actualización.  
  
**Acción en el cambio de objeto remoto**  
Especifica el valor predeterminado en el cuadro de diálogo de sincronización cuando los objetos cambian en el servidor de base de datos.  El conjunto de valores predeterminado es **actualizar desde la base de datos**.  
  
-   Si selecciona **actualizar desde base de**datos, SSMA cargará las definiciones de base de datos en los metadatos cuando se cumpla la condición.  
  
-   Si selecciona **escribir en la base**de datos, SSMA actualizará el objeto en la base de datos según el contenido de los metadatos de SSMA cuando se cumpla la condición.  
  
-   Si selecciona **omitir**, SSMA no realizará ninguna acción de actualización.  
  
**Acción cuando faltan metadatos de objeto local**  
Especifica el valor predeterminado en el cuadro de diálogo de sincronización cuando faltan metadatos locales. El conjunto de valores predeterminado es **actualizar desde la base de datos**.  
  
-   Si selecciona **actualizar desde base de datos**, SSMA selecciona la opción **actualizar desde la base de datos** cuando se cumple la condición.  
  
-   Si selecciona **escribir en la base de datos**, SSMA eliminará el objeto de la base de datos cuando se cumpla la condición.  
  
-   Si selecciona **omitir**, SSMA no realizará ninguna acción de actualización.  
  
