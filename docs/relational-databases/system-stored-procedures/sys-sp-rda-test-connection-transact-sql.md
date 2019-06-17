---
title: sys.sp_rda_test_connection (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_test_connection
- sys.sp_rda_test_connection_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_test_connection stored procedure
ms.assetid: e2ba050c-d7e3-4f33-8281-c9b525b4edb4
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: cdf171c66c19d87ea4919eeb55dca65f14b89ebd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65982876"
---
# <a name="syssprdatestconnection-transact-sql"></a>sys.sp_rda_test_connection (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Prueba la conexión de SQL Server para el servidor remoto de Azure y notifica problemas que pueden impedir que la migración de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
EXECUTE sys.sp_rda_test_connection  
   @database_name = N'db_name',   
   @server_address = N'azure_server_fully_qualified_address',  
   @azure_username = N'azure_username',   
   @azure_password = N'azure_password',  
   @credential_name = N'credential_name'  
  
```  
  
## <a name="arguments"></a>Argumentos  
 @database_name = N'*db_name*'  
 El nombre de la base de datos de SQL Server habilitada para Stretch. Este parámetro es opcional.  
  
 @server_address = N'*azure_server_fully_qualified_address*'  
 La dirección completa del servidor de Azure.  
  
-   Si proporciona un valor para **@database_name** , pero la base de datos especificado no está habilitada para Stretch, entonces tendrá que proporcionar un valor para **@server_address** .  
  
-   Si proporciona un valor para **@database_name** y la base de datos habilitadas para Stretch, entonces no tendrá que proporcionar un valor para **@server_address** . Si proporciona un valor para **@server_address** , el procedimiento almacenado pasa por alto y utiliza existente de servidor de Azure ya asociado a la base de datos habilitadas para Stretch.  
  
 @azure_username = N'*azure_username*  
 El nombre de usuario para el servidor remoto de Azure.  
  
 @azure_password = N'*azure_password*'  
 La contraseña para el servidor remoto de Azure.  
  
 @credential_name = N'*credential_name*'  
 En lugar de proporcionar un nombre de usuario y una contraseña, puede proporcionar el nombre de una credencial almacenada en la base de datos habilitadas para Stretch.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 En caso de **éxito**, sp_rda_test_connection devuelve el error 14855 (STRETCH_MAJOR, STRETCH_CONNECTION_TEST_PROC_SUCCEEDED) con una gravedad EX_INFO y código de retorno de un estado correcto.  
  
 En caso de **error**, sp_rda_test_connection devuelve el error 14856 (STRETCH_MAJOR, STRETCH_CONNECTION_TEST_PROC_FAILED) con una gravedad EX_USER y código de retorno de un error.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|link_state|INT|Uno de los valores siguientes, que corresponden a los valores de **link_state_desc**.<br /><br /> -   0<br />-   1<br />-   2<br />-   3<br />-   4|  
|link_state_desc|varchar(32)|Uno de los valores siguientes, que corresponden a los anteriores valores para **link_state**.<br /><br /> -CORRECTO<br />     El entre SQL Server y Azure remoto servidor es correcto.<br />-   ERROR_AZURE_FIREWALL<br />     El firewall de Azure impide el vínculo entre SQL Server y el servidor remoto de Azure.<br />-ERROR_NO_CONNECTION<br />     SQL Server no se puede establecer una conexión con el servidor remoto de Azure.<br />-   ERROR_AUTH_FAILURE<br />     Un error de autenticación está impidiendo que el vínculo entre SQL Server y el servidor remoto de Azure.<br />-ERROR<br />     Un error que no es un problema de autenticación, un problema de conectividad o un problema de firewall impide que el vínculo entre SQL Server y el servidor remoto de Azure.|  
|error_number|INT|El número del error. Si no hay ningún error, este campo es NULL.|  
|error_message|nvarchar(1024)|Mensaje de error. Si no hay ningún error, este campo es NULL.|  
  
## <a name="permissions"></a>Permisos  
 Se requieren permisos db_owner.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="check-the-connection-from-sql-server-to-the-remote-azure-server"></a>Compruebe la conexión de SQL Server para el servidor remoto de Azure  
  
```sql  
EXECUTE sys.sp_rda_test_connection @database_name = N'<Stretch-enabled database>'  
GO  
  
```  
  
 Los resultados muestran que SQL Server no se puede conectar al servidor remoto de Azure.  
  
|link_state|link_state_desc|error_number|error_message|  
|-----------------|-----------------------|-------------------|--------------------|  
|2|ERROR_NO_CONNECTION|*\<número de error relacionados con la conexión >*|*\<mensaje de error relacionados con la conexión >*|  
  
### <a name="check-the-azure-firewall"></a>Compruebe el firewall de Azure  
  
```sql  
USE <Stretch-enabled database>  
GO  
EXECUTE sys.sp_rda_test_connection  
GO  
  
```  
  
 Los resultados muestran que el firewall de Azure impide el vínculo entre SQL Server y el servidor remoto de Azure.  
  
|link_state|link_state_desc|error_number|error_message|  
|-----------------|-----------------------|-------------------|--------------------|  
|1|ERROR_AZURE_FIREWALL|*\<número de error relacionado con el servidor de seguridad >*|*\<mensaje de error relacionado con el servidor de seguridad >*|  
  
### <a name="check-authentication-credentials"></a>Compruebe las credenciales de autenticación  
  
```sql  
USE <Stretch-enabled database>  
GO  
EXECUTE sys.sp_rda_test_connection  
GO  
  
```  
  
 Los resultados muestran que un error de autenticación impide que el vínculo entre SQL Server y el servidor remoto de Azure.  
  
|link_state|link_state_desc|error_number|error_message|  
|-----------------|-----------------------|-------------------|--------------------|  
|3|ERROR_AUTH_FAILURE|*\<número de error relacionados con la autenticación >*|*\<mensaje de error relacionados con la autenticación >*|  
  
### <a name="check-the-status-of-the-remote-azure-server"></a>Comprobar el estado del servidor remoto de Azure  
  
```sql  
USE <SQL Server database>  
GO  
EXECUTE sys.sp_rda_test_connection   
    @server_address = N'<server name>.database.windows.net',   
    @azure_username = N'<user name>',   
    @azure_password = N'<password>'  
GO  
  
```  
  
 Los resultados muestran que la conexión es correcta y que puede habilitar Stretch Database para la base de datos especificado.  
  
|link_state|link_state_desc|error_number|error_message|  
|-----------------|-----------------------|-------------------|--------------------|  
|0|HEALTHY|NULL|NULL|  
  
  
