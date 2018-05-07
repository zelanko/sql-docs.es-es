---
title: sp_configure (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/16/2016
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_configure
- sp_configure_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_configure
ms.assetid: d18b251d-b37a-4f5f-b50c-502d689594c8
caps.latest.revision: 60
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 05074a051f39e8b2dd81314ed6e230868c410c49
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="spconfigure-transact-sql"></a>sp_configure (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/t-sql-appliesto-ss-asdbmi-xxxx-pwd-md.md)]

  Muestra o cambia las opciones de configuración global del servidor actual.

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]
  
> [!NOTE]  
>  Para opciones de configuración de nivel de base de datos, vea [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md). Para configurar NUMA de software, consulte [Soft-NUMA &#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server  
  
sp_configure [ [ @configname = ] 'option_name'   
    [ , [ @configvalue = ] 'value' ] ]  
```  
  
```  
-- Syntax for Parallel Data Warehouse  
  
-- List all of the configuration options  
sp_configure  
[;]  
  
-- Configure Hadoop connectivity  
sp_configure [ @configname= ] 'hadoop connectivity',  
             [ @configvalue = ] { 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 }  
[;]  
RECONFIGURE  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@configname=** ] **'***nombre_de_opción***'**  
 Es el nombre de una opción de configuración. *option_name* es **varchar(35)** y su valor predeterminado es NULL. [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] reconoce cualquier cadena única que forme parte del nombre de configuración. Si no se especifica, se devuelve la lista completa de opciones.  
  
 Para obtener información acerca de las opciones de configuración disponibles y sus valores, vea [opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
 [ **@configvalue=** ] **'***valor***'**  
 Es la nueva configuración. *value* es de tipo **int**y su valor predeterminado es NULL. El valor máximo depende de la opción individual.  
  
 Para ver el valor máximo para cada opción, vea el **máximo** columna de la **sys.configurations** vista de catálogo.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Cuando se ejecuta sin parámetros, **sp_configure** devuelve un conjunto de resultados con cinco columnas y ordena las opciones alfabéticamente en orden ascendente, tal como se muestra en la tabla siguiente.  
  
 Los valores de **config_value** y **run_value** no son equivalentes de forma automática. Después de actualizar un valor de configuración mediante el uso de **sp_configure**, el administrador del sistema debe actualizar el valor de configuración actual mediante RECONFIGURE o RECONFIGURE WITH OVERRIDE. Para obtener más información, vea la sección Comentarios.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**Nombre**|**nvarchar(35)**|Nombre de la opción de configuración.|  
|**Mínimo**|**int**|Valor mínimo de la opción de configuración.|  
|**Máximo**|**int**|Valor máximo de la opción de configuración.|  
|**config_value**|**int**|Valor al que se ha configurado la opción de configuración con **sp_configure** (valor en **sys.configurations.value**). Para obtener más información acerca de estas opciones, consulte [opciones de configuración de servidor &#40;SQL Server&#41; ](../../database-engine/configure-windows/server-configuration-options-sql-server.md) y [sys.configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md).|  
|**run_value**|**int**|Valor de la opción de configuración (valor en **sys.configurations.value_in_use**).<br /><br /> Para obtener más información, consulte [sys.configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md).|  
  
## <a name="remarks"></a>Comentarios  
 Use **sp_configure** para mostrar o cambiar la configuración de nivel de servidor. Para cambiar la configuración de la base de datos, utilice ALTER DATABASE. Para cambiar la configuración que afecta solo a la sesión de usuario actual, utilice la instrucción SET.  
  
## <a name="updating-the-running-configuration-value"></a>Actualizar el valor de configuración actual  
 Cuando se especifica un nuevo *valor* para un *opción*, el conjunto de resultados muestra este valor en el **config_value** columna. Este valor difiere inicialmente el valor de la **run_value** columna, que muestra el valor de configuración que se está ejecutando. Para actualizar el valor de configuración de ejecución en el **run_value** columna, el administrador del sistema debe ejecutar RECONFIGURE o RECONFIGURE WITH OVERRIDE.  
  
 RECONFIGURE y RECONFIGURE WITH OVERRIDE funcionan con todas las opciones de configuración. No obstante, la instrucción RECONFIGURE básica rechaza cualquier valor de opción que esté fuera de un intervalo razonable o que pueda ocasionar conflictos entre las opciones. Por ejemplo, RECONFIGURE genera un error si la **intervalo de recuperación** valor es mayor que 60 minutos o si la **máscara de afinidad** se superpone con el **máscara de afinidad de E/S**valor. RECONFIGURE WITH OVERRIDE, por el contrario, admite cualquier valor de opción que contenga el tipo de datos correcto y obliga a realizar la reconfiguración con el valor especificado.  
  
> [!CAUTION]  
>  Un valor de opción inapropiado puede afectar negativamente a la configuración de la instancia de servidor. Utilice RECONFIGURE WITH OVERRIDE con precaución.  
  
 La instrucción RECONFIGURE actualiza algunas opciones dinámicamente; para otras opciones es necesario detener y reiniciar el servidor. Por ejemplo, el **memoria de servidor mínima** y **memoria de servidor máxima** opciones de memoria del servidor se actualizan dinámicamente en el [!INCLUDE[ssDE](../../includes/ssde-md.md)]; por lo tanto, puede cambiar sin necesidad de reiniciar el servidor. En cambio, reconfigurar el valor actual de la **factor de relleno** opción requiere reiniciar el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 Tras ejecutar RECONFIGURE en una opción de configuración, puede ver si la opción se ha actualizado dinámicamente ejecutando **sp_configure'***option_name***'**. Los valores de la **run_value** y **config_value** deben coincidir con las columnas de una opción actualizada dinámicamente. También puede comprobar para ver qué opciones son dinámicas mirando la **is_dynamic** columna de la **sys.configurations** vista de catálogo.  
  
> [!NOTE]  
>  Si un determinado *valor* es demasiado alto para una opción, el **run_value** columna refleja el hecho de que el [!INCLUDE[ssDE](../../includes/ssde-md.md)] se establece de forma predeterminada en la memoria dinámica en lugar de usar un parámetro que no es válido.  
  
 Para obtener más información, consulte [volver a configurar &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md).  
  
## <a name="advanced-options"></a>Opciones avanzadas  
 Algunas opciones de configuración, como **máscara de afinidad** y **intervalo de recuperación**, se designan como opciones avanzadas. De forma predeterminada, estas opciones no están disponibles para verlas o modificarlas. Para que estén disponibles, establezca el **ShowAdvancedOptions** opción de configuración en 1.  
  
 Para obtener más información acerca de las opciones de configuración y sus valores, vea [opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
## <a name="permissions"></a>Permissions  
 De forma predeterminada, todos los usuarios tienen permisos de ejecución en **sp_configure** sin ningún parámetro o solo con el primero. Para ejecutar **sp_configure** con ambos parámetros para cambiar una opción de configuración o para ejecutar la instrucción RECONFIGURE, debe tener concedido el permiso de nivel de servidor de ALTER SETTINGS. Los roles fijos de servidor **sysadmin** y **serveradmin** tienen el permiso ALTER SETTINGS de forma implícita.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-listing-the-advanced-configuration-options"></a>A. Enumerar las opciones de configuración avanzadas  
 En este ejemplo se muestra cómo establecer y enumerar todas las opciones de configuración. Para ver las opciones de configuración avanzadas, primero hay que establecer en `show advanced option` el valor de `1`. A continuación, si se ejecuta `sp_configure` sin parámetros, se mostrarán todas las opciones de configuración.  
  
```  
USE master;  
GO  
EXEC sp_configure 'show advanced option', '1';  
```  
  
 Este es el mensaje: "Se ha cambiado la opción de configuración 'show advanced options' de 0 a 1. Ejecute la instrucción RECONFIGURE para instalar".  
  
 Ejecute `RECONFIGURE` y muestre todas las opciones de configuración:  
  
```  
RECONFIGURE;  
EXEC sp_configure;  
```  
  
### <a name="b-changing-a-configuration-option"></a>B. Cambiar una opción de configuración  
 En el siguiente ejemplo se establece el `recovery interval` (intervalo de recuperación) del sistema en `3` minutos.  
  
```  
USE master;  
GO  
EXEC sp_configure 'recovery interval', '3';  
RECONFIGURE WITH OVERRIDE;  
```  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-list-all-available-configuration-settings"></a>C. Lista de todas las opciones de configuración disponibles  
 En este ejemplo se muestra cómo enumerar todas las opciones de configuración.  
  
```  
EXEC sp_configure;  
```  
  
 El resultado devuelve el nombre de opción seguido por los valores mínimo y máximo de la opción. El **config_value** es el valor que [!INCLUDE[ssDW](../../includes/ssdw-md.md)] va a usar cuando se completa la reconfiguración. El valor **run_value** es el valor que se está usando actualmente. Los valores **config_value** y **run_value** son normalmente los mismos, a menos que el valor se esté modificando.  
  
### <a name="d-list-the-configuration-settings-for-one-configuration-name"></a>D. Lista de las opciones de configuración para un nombre de configuración  
  
```  
EXEC sp_configure @configname='hadoop connectivity';  
```  
  
### <a name="e-set-hadoop-connectivity"></a>E. Establecer la conectividad de Hadoop  
 La configuración de conectividad de Hadoop requiere algunos pasos más además de ejecutar sp_configure. Para conocer el procedimiento completo, consulte [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md).  
  
## <a name="see-also"></a>Vea también  
 [RECONFIGURE & #40; Transact-SQL & #41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Instrucciones SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.configurations&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)   
 [Soft-NUMA &#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)  
  
  
