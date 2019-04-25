---
title: Proyecto (sincronización) (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: e223fb7d-05ec-4fa5-8973-d845c33a23dd
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: fe71e5b301c016e25bb179e0104831285dab3ce1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62628691"
---
# <a name="project-settingssynchronization-oracletosql"></a>Configuración del proyecto (sincronización) (OracleToSQL)
La página de sincronización de la **configuración del proyecto** cuadro de diálogo contiene la configuración que permiten personalizar cómo SSMA carga y las actualizaciones de la base de datos, como tablas y procedimientos almacenados, los objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Las opciones de acciones predeterminadas especifican la configuración predeterminada para actualizar objetos de la base de datos de Oracle y para la sincronización de objetos con la base de datos de SQL Server. Para obtener más información, consulte [actualizar desde la base de datos: Oracle](../../ssma/oracle/refresh-from-database-oracletosql.md).  
  
Puede tener acceso a dos páginas diferentes de sincronización que contienen los mismos valores:  
  
-   Para especificar la configuración para todos los proyectos SSMA futuros, en el **herramientas** menú, haga clic en **la configuración predeterminada del proyecto**y, a continuación, haga clic en **sincronización** en la parte inferior del panel izquierdo.  
  
-   Para especificar la configuración para el proyecto actual, en el **herramientas** menú, haga clic en **configuración del proyecto**y, a continuación, haga clic en **sincronización** en la parte inferior del panel izquierdo.  
  
## <a name="miscellaneous-options"></a>Otras opciones  
**Intentos**  
Especifica el número de intentos de SSMA debe realizar cuando se carga en los objetos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los objetos que no se cargan en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el intento actual volverá a intentarse hasta SSMA alcanza el número máximo de intentos en el proceso de sincronización actual. Establecido un valor predeterminado es **2**  
  
## <a name="synchronization-for-oracle-options"></a>Sincronización de las opciones de Oracle  
**Acción de cambio de los objetos locales y remotos**  
Especifica la configuración predeterminada en el cuadro de diálogo de sincronización cuando la definición del objeto cambia de SSMA y en el servidor de base de datos. Establecido un valor predeterminado es **actualizar desde la base de datos**.  
  
-   Si selecciona **actualizar desde la base de datos**, SSMA cargará las definiciones de base de datos en los metadatos cuando se cumple la condición.  
  
-   Si selecciona **Skip**, SSMA no realizará ninguna acción de actualización.  
  
**Acción de cambio de objeto local**  
Especifica la configuración predeterminada en el cuadro de diálogo de sincronización cuando cambia el objeto en SSMA. Establecido un valor predeterminado es **Skip**.  
  
-   Si selecciona **actualizar desde la base de datos**, SSMA cargará las definiciones de base de datos en los metadatos cuando se cumple la condición.  
  
-   Si selecciona **Skip**, SSMA no realizará ninguna acción de actualización.  
  
**Acción de cambio de objeto remoto**  
Especifica la configuración predeterminada en el cuadro de diálogo de sincronización cuando cambian los objetos en el servidor de base de datos. Establecido un valor predeterminado es **actualizar desde la base de datos**.  
  
-   Si selecciona **actualizar desde la base de datos**, SSMA cargará las definiciones de base de datos en los metadatos cuando se cumple la condición.  
  
-   Si selecciona **Skip**, SSMA no realizará ninguna acción de actualización.  
  
**Acción cuando faltan los metadatos del objeto local**  
Especifica la configuración predeterminada en el cuadro de diálogo de sincronización cuando faltan los metadatos locales. Establecido un valor predeterminado es **actualizar desde la base de datos**.  
  
-   Si selecciona **actualizar desde la base de datos**, SSMA cargará las definiciones de base de datos en los metadatos cuando se cumple la condición.  
  
-   Si selecciona **Skip**, SSMA no realizará ninguna acción de actualización.  
  
## <a name="synchronization-for-sql-server-options"></a>Sincronización de las opciones de SQL Server  
**Acción de cambio de los objetos locales y remotos**  
Especifica la configuración predeterminada en el cuadro de diálogo de sincronización cuando la definición del objeto cambia de SSMA y en el servidor de base de datos. Establecido un valor predeterminado es **escritura a la base de datos**.  
  
-   Si selecciona **actualizar desde la base de datos**, SSMA cargará las definiciones de base de datos en los metadatos cuando se cumple la condición.  
  
-   Si selecciona **escribir en la base de datos**, SSMA actualizará los objetos de la base de datos según el contenido de los metadatos SSMA cuando se cumple la condición.  
  
-   Si selecciona **Skip**, SSMA no realizará ninguna acción de actualización.  
  
**Acción de cambio de objeto local**  
Especifica la configuración predeterminada en el cuadro de diálogo de sincronización cuando cambia el objeto en SSMA. Establecido un valor predeterminado es **escritura a la base de datos**.  
  
-   Si selecciona **actualizar desde la base de datos**, SSMA cargará las definiciones de base de datos en los metadatos cuando se cumple la condición.  
  
-   Si selecciona **escribir en la base de datos**, SSMA actualizará el objeto en la base de datos según el contenido de los metadatos SSMA cuando se cumple la condición.  
  
-   Si selecciona **Skip**, SSMA no realizará ninguna acción de actualización.  
  
**Acción de cambio de objeto remoto**  
Especifica la configuración predeterminada en el cuadro de diálogo de sincronización cuando cambian los objetos en el servidor de base de datos.  Establecido un valor predeterminado es **actualizar desde la base de datos**.  
  
-   Si selecciona **actualizar desde la base de datos**, SSMA cargará las definiciones de base de datos en los metadatos cuando se cumple la condición.  
  
-   Si selecciona **escribir en la base de datos**, SSMA actualizará el objeto en la base de datos según el contenido de los metadatos SSMA cuando se cumple la condición.  
  
-   Si selecciona **Skip**, SSMA no realizará ninguna acción de actualización.  
  
**Acción cuando faltan los metadatos del objeto local**  
Especifica la configuración predeterminada en el cuadro de diálogo de sincronización cuando faltan los metadatos locales. Establecido un valor predeterminado es **actualizar desde la base de datos**.  
  
-   Si selecciona **actualizar desde la base de datos**, SSMA selecciona el **actualizar desde la base de datos** opción cuando se cumple la condición.  
  
-   Si selecciona **escribir en la base de datos**, SSMA eliminará el objeto de la base de datos cuando se cumple la condición.  
  
-   Si selecciona **Skip**, SSMA no realizará ninguna acción de actualización.  
  
