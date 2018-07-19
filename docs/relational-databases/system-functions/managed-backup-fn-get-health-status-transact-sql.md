---
title: managed_backup.fn_get_health_status (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- fn_get_health_status_TSQL
- smart_admin.fn_get_health_status_TSQL
- smart_admin.fn_get_health_status
- fn_get_health_status
dev_langs:
- TSQL
helpviewer_keywords:
- smart_admin.fn_get_health_status
- fn_get_health_status
ms.assetid: b376711d-444a-4b5e-b483-8df323b4e31f
caps.latest.revision: 12
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0fa9a510f2be08329173898b7e0e6794458ea8fe
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38041973"
---
# <a name="managedbackupfngethealthstatus-transact-sql"></a>managed_backup.fn_get_health_status (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Devuelve una tabla de cero, una o más filas del recuento agregado de los errores notificados por Eventos extendidos para un período de tiempo concreto.  
  
 La función se utiliza para informar del estado de mantenimiento de los servicios en Administración inteligente.  Actualmente [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] se admite bajo el paraguas de Administración inteligente. Por tanto, los errores devueltos se relacionan con [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].  
  
 
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
managed_backup.fn_get_health_status([@begin_time = ] 'time_1' , [ @end_time = ] 'time_2')  
```  
  
##  <a name="Arguments"></a> Argumentos  
 [@begin_time]  
 El inicio del período de tiempo desde el que se calcula el recuento agregado de los errores.  El @begin_time parámetro es DATETIME. El valor predeterminado es NULL. Si el valor es NULL, la función procesará los eventos notificados al menos 30 minutos antes de la hora actual.  
  
 [ @end_time]  
 El fin del período de tiempo desde el que se calcula el recuento agregado de los errores. El @end_time parámetro es DateTime y su valor predeterminado es null. Si el valor es NULL, la función procesará los eventos extendidos al menos hasta el momento actual.  
  
## <a name="table-returned"></a>Tabla devuelta  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|number_of_storage_connectivity_errors|INT|Número de errores de conexión cuando el programa se conecta a la cuenta de Almacenamiento de Windows Azure.|  
|number_of_sql_errors|INT|Número de errores devueltos cuando el programa se conecta al Motor de SQL Server.|  
|number_of_invalid_credential_errors|INT|Número de errores devueltos cuando el programa intenta autenticarse utilizando las credenciales SQL.|  
|number_of_other_errors|INT|Número de errores en otras categorías además de conectividad, SQL o credencial.|  
|number_of_corrupted_or_deleted_backups|INT|Número de archivos de copia de seguridad dañados o eliminados.|  
|number_of_backup_loops|INT|Número de veces que el agente de copia de seguridad examina todas las bases de datos configuradas con [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].|  
|number_of_retention_loops|INT|El número de veces que las bases de datos se examinan para evaluar el período de retención establecido.|  
  
## <a name="best-practices"></a>Procedimientos recomendados  
 Estos recuentos agregados se pueden utilizar para supervisar el estado del sistema. Por ejemplo, si la columna number_ of_retention_loops es 0 en 30 minutos, es posible que la administración de la retención esté tardando mucho o incluso que no funcione correctamente. Las columnas de errores que no son cero pueden indicar que hay problemas y los registros de Eventos extendidos se deben comprobar para conocerlos. Como alternativa, use el procedimiento almacenado **managed_backup.sp_get_backup_diagnostics** para obtener una lista de eventos extendidos para encontrar los detalles del error.  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permisos  
 Requiere **seleccione** permisos en la función.  
  
## <a name="examples"></a>Ejemplos  
  
-   El ejemplo siguiente devuelve los recuentos de errores agregados para los 30 últimos minutos desde el momento en que se ejecutó.  
  
    ```  
    SELECT *  
    FROM managed_backup.fn_get_health_status(NULL, NULL)  
  
    ```  
  
-   El ejemplo siguiente devuelve el recuento de errores agregados para la semana actual:  
  
    ```  
    Use msdb  
    Go  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)   
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
    SELECT *  
    FROM managed_backup.fn_get_health_status(@startofweek, @endofweek)  
  
    ```  
  
  
