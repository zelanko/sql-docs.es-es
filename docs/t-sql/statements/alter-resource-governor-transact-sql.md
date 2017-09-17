---
title: MODIFICAR REGULADOR de recursos (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 05/01/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER RESOURCE GOVERNOR
- ALTER_RESOURCE_GOVERNOR_TSQL
- ALTER RESOURCE GOVERNOR RECONFIGURE
- ALTER_RESOURCE_GOVERNOR_RECONFIGURE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER RESOURCE GOVERNOR
- RECONFIGURE, ALTER RESOURCE GOVERNOR
ms.assetid: 442c54bf-a0a6-4108-ad20-db910ffa6e3c
caps.latest.revision: 49
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ac7ae791ec7867b13a8547ec60436f25536cd5b7
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="alter-resource-governor-transact-sql"></a>ALTER RESOURCE GOVERNOR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Esta instrucción se usa para realizar las siguientes acciones de regulador de recursos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Aplicar los cambios de configuración especificados al crear | ALTER | DROP WORKLOAD GROUP o CREATE | ALTER | DROP RESOURCE POOL o CREATE | ALTER | Se emiten las instrucciones DROP EXTERNAL RESOURCE POOL.  
  
-   Habilitar o deshabilitar el regulador de recursos.  
  
-   Configurar la clasificación de las solicitudes entrantes.  
  
-   Restablece las estadísticas de los grupos de cargas de trabajo y los grupos de recursos.  
  
-   Establece la cantidad máxima de operaciones de E/S por volumen de disco.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
ALTER RESOURCE GOVERNOR   
      { DISABLE | RECONFIGURE }  
    | WITH ( CLASSIFIER_FUNCTION = { schema_name.function_name | NULL } )  
    | RESET STATISTICS  
    | WITH ( MAX_OUTSTANDING_IO_PER_VOLUME = value )   
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 DISABLE  
 Deshabilita el regulador de recursos. Deshabilitar el regulador de recursos tiene los siguientes resultados:  
  
-   No se ejecuta la función clasificadora.  
  
-   Todas las conexiones nuevas se clasifican automáticamente en el grupo predeterminado.  
  
-   Las solicitudes iniciadas por el sistema se clasifican en el grupo de cargas de trabajo interno.  
  
-   Se restablecen los valores predeterminados de todas las configuraciones existentes del grupo de cargas de trabajo y el grupo de recursos de servidor. En este caso, no se desencadena ningún evento cuando se alcanzan los límites.  
  
-   La supervisión normal del sistema no resulta afectada.  
  
-   Se pueden realizar cambios de configuración, pero los cambios no surtirán efecto hasta que se habilite el regulador de recursos.  
  
-   Al reiniciar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el regulador de recursos no cargará su configuración, sino que tendrá únicamente los grupos de cargas de trabajo y los grupos de recursos de servidor predeterminados e internos.  
  
 RECONFIGURE  
 Si el regulador de recursos no está habilitado, RECONFIGURE lo habilita. Habilitar el regulador de recursos tiene los siguientes resultados:  
  
-   La función clasificadora se ejecuta para las nuevas conexiones, de forma que se puede asignar su carga de trabajo a los grupos de cargas de trabajo.  
  
-   Se respetan y se aplican los límites de los recursos especificados en la configuración del regulador de recursos.  
  
-   Las solicitudes que existieran antes de habilitar el regulador de recursos resultarán afectadas por los cambios de configuración que se realizaron cuando se deshabilita el regulador de recursos.  
  
 Cuando se ejecuta el regulador de recursos, RECONFIGURE aplica cualquier configuración cambios solicitan al crear | ALTER | DROP WORKLOAD GROUP o CREATE | ALTER | DROP RESOURCE POOL o CREATE | ALTER | Se ejecutan las instrucciones DROP EXTERNAL RESOURCE POOL.  
  
> [!IMPORTANT]  
>  Debe enviarse ALTER RESOURCE GOVERNOR RECONFIGURE para que surtan efecto los cambios en la configuración.  
  
 CLASSIFIER_FUNCTION = { *schema_name***.** *function_name* | NULL}  
 Registra la función de clasificación especificada por *schema_name.function_name*. Esta función clasifica cada sesión nueva y asigna las solicitudes de sesión y las consultas para un grupo de cargas de trabajo. Si se usa NULL, las nuevas sesiones se asignan automáticamente al grupo de cargas de trabajo predeterminado.  
  
 RESET STATISTICS  
 Restablece las estadísticas en todos los grupos de cargas de trabajo y los grupos de recursos. Para obtener más información, consulte [sys.dm_resource_governor_workload_groups &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md) y [sys.dm_resource_governor_resource_pools &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md).  
  
 MAX_OUTSTANDING_IO_PER_VOLUME = *valor*  
 **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Establece la cantidad máxima de operaciones de E/S en cola por volumen de disco. Estas operaciones de E/S pueden ser lecturas o escrituras de cualquier tamaño.  El valor máximo de MAX_OUTSTANDING_IO_PER_VOLUME es 100. No es un porcentaje. Este valor está diseñado para optimizar el regulador de recursos de E/S según las características de E/S de un volumen de disco. Se recomienda experimentar con distintos valores y considere la posibilidad de usar una herramienta de calibración como IOMeter, [DiskSpd](https://gallery.technet.microsoft.com/DiskSpd-a-robust-storage-6cd2f223), o SQLIO (en desuso) para identificar el valor máximo para el subsistema de almacenamiento. Este valor proporciona una comprobación de seguridad de nivel de sistema que permite a SQL Server cumplir el mínimo de IOPS para los grupos de recursos aunque otros grupos tengan el valor de MAX_IOPS_PER_VOLUME establecido en ilimitado. Para obtener más información sobre MAX_IOPS_PER_VOLUME, vea [CREATE RESOURCE POOL](../../t-sql/statements/create-resource-pool-transact-sql.md).  
  
## <a name="remarks"></a>Comentarios  
 ALTER RESOURCE GOVERNOR DISABLE, ALTER RESOURCE GOVENOR RECONFIGURE y ALTER RESOURCE GOVERNOR RESET STATISTICS no se pueden usar en una transacción de usuario.  
  
 El parámetro RECONFIGURE forma parte de la sintaxis del regulador de recursos y no debe confundirse con [volver a configurar](../../t-sql/language-elements/reconfigure-transact-sql.md), que es una instrucción DDL independiente.  
  
 Se recomienda familiarizarse con los estados del regulador de recursos antes de ejecutar las instrucciones de DDL. Para obtener más información, consulte [regulador de recursos](../../relational-databases/resource-governor/resource-governor.md).  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso CONTROL SERVER.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-starting-the-resource-governor"></a>A. Iniciar el regulador de recursos  
 La primera vez que se instala [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el regulador de recursos está deshabilitado. En el ejemplo siguiente, se inicia regulador de recursos. Después de ejecutar la instrucción, el regulador de recursos se ejecuta y puede usar los grupos de recursos de servidor y los grupos de cargas de trabajo predefinidos.  
  
```  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
```  
  
### <a name="b-assigning-new-sessions-to-the-default-group"></a>B. Asignar nuevas sesiones al grupo predeterminado  
 En el ejemplo siguiente, se asignan todas las sesiones nuevas al grupo de cargas de trabajo predeterminado; para ello, se quitan las funciones clasificadoras existentes de la configuración del regulador de recursos. Cuando no se designa ninguna función como función clasificadora, todas las sesiones nuevas se asignan al grupo de cargas de trabajo predeterminado. Este cambio solo se aplica a las sesiones nuevas. Las sesiones existentes no resultan afectadas.  
  
```  
ALTER RESOURCE GOVERNOR WITH (CLASSIFIER_FUNCTION = NULL);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
```  
  
### <a name="c-creating-and-registering-a-classifier-function"></a>C. Crear y registrar una función clasificadora  
 En el ejemplo siguiente, se crea una función clasificadora denominada `dbo.rgclassifier_v1`. La función clasifica cada nueva sesión basándose en el nombre de usuario o en el nombre de aplicación y asigna las solicitudes de sesión y las consultas a un grupo de cargas de trabajo concreto. Las sesiones que no se corresponden con los nombres de usuario o de aplicación especificados se asignan al grupo de cargas de trabajo predeterminado. A continuación, se registra la función clasificadora y se aplica el cambio de configuración.  
  
```  
-- Store the classifier function in the master database.  
USE master;  
GO  
SET ANSI_NULLS ON;  
GO  
SET QUOTED_IDENTIFIER ON;  
GO  
CREATE FUNCTION dbo.rgclassifier_v1() RETURNS sysname   
WITH SCHEMABINDING  
AS  
BEGIN  
-- Declare the variable to hold the value returned in sysname.  
    DECLARE @grp_name AS sysname  
-- If the user login is 'sa', map the connection to the groupAdmin  
-- workload group.   
    IF (SUSER_NAME() = 'sa')  
        SET @grp_name = 'groupAdmin'  
-- Use application information to map the connection to the groupAdhoc  
-- workload group.  
    ELSE IF (APP_NAME() LIKE '%MANAGEMENT STUDIO%')  
        OR (APP_NAME() LIKE '%QUERY ANALYZER%')  
            SET @grp_name = 'groupAdhoc'  
-- If the application is for reporting, map the connection to  
-- the groupReports workload group.  
    ELSE IF (APP_NAME() LIKE '%REPORT SERVER%')  
        SET @grp_name = 'groupReports'  
-- If the connection does not map to any of the previous groups,  
-- put the connection into the default workload group.  
    ELSE  
        SET @grp_name = 'default'  
    RETURN @grp_name  
END;  
GO  
-- Register the classifier user-defined function and update the   
-- the in-memory configuration.  
ALTER RESOURCE GOVERNOR WITH (CLASSIFIER_FUNCTION=dbo.rgclassifier_v1);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
### <a name="d-resetting-statistics"></a>D. Restablecer las estadísticas  
 En el ejemplo siguiente, se restablecen las estadísticas de todos los grupos de cargas de trabajo y los grupos de recursos.  
  
```  
ALTER RESOURCE GOVERNOR RESET STATISTICS;  
```  
  
### <a name="e-setting-the-maxoutstandingiopervolume-option"></a>E. Establecer la opción MAX_OUTSTANDING_IO_PER_VOLUME  
 En el ejemplo siguiente se establece la opción MAX_OUTSTANDING_IO_PER_VOLUME en 20.  
  
```  
ALTER RESOURCE GOVERNOR  
WITH (MAX_OUTSTANDING_IO_PER_VOLUME = 20);   
```  
  
## <a name="see-also"></a>Vea también  
 [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)   
 [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)   
 [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)   
 [DROP EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-external-resource-pool-transact-sql.md)   
 [Modificar grupo de recursos externo &#40; Transact-SQL &#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)   
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)   
 [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)   
 [Regulador de recursos](../../relational-databases/resource-governor/resource-governor.md)   
 [Sys.dm_resource_governor_workload_groups &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md)   
 [Sys.dm_resource_governor_resource_pools &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md)  
  
  

