---
title: Sys. sp_rda_test_connection (Transact-SQL) | Microsoft Docs
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
ms.openlocfilehash: 69b3b9eae6c292b9501dfbe74b84d7399304a291
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "72305157"
---
# <a name="syssp_rda_test_connection-transact-sql"></a>Sys. sp_rda_test_connection (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Prueba la conexión desde SQL Server al servidor remoto de Azure e informa de los problemas que pueden impedir la migración de datos.  
  
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
 @database_name= N '*db_name*'  
 Nombre de la base de datos de SQL Server habilitada para Stretch. Este parámetro es opcional.  
  
 @server_address= N '*azure_server_fully_qualified_address*'  
 La dirección completa del servidor de Azure.  
  
-   Si proporciona un valor para ** \@database_name**, pero la base de datos especificada no está habilitada para Stretch, tendrá que proporcionar un valor para ** \@SERVER_ADDRESS**.  
  
-   Si proporciona un valor para ** \@database_name**y la base de datos especificada está habilitada para Stretch, no tiene que proporcionar un valor para ** \@SERVER_ADDRESS**. Si proporciona un valor para ** \@SERVER_ADDRESS**, el procedimiento almacenado lo omite y usa el servidor de Azure existente que ya está asociado a la base de datos habilitada para Stretch.  
  
 @azure_username= N '*azure_username*  
 El nombre de usuario para el servidor remoto de Azure.  
  
 @azure_password= N '*azure_password*'  
 La contraseña para el servidor remoto de Azure.  
  
 @credential_name= N '*credential_name*'  
 En lugar de proporcionar un nombre de usuario y una contraseña, puede proporcionar el nombre de una credencial almacenada en la base de datos habilitada para Stretch.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 En caso de **éxito**, sp_rda_test_connection devuelve el error 14855 (STRETCH_MAJOR, STRETCH_CONNECTION_TEST_PROC_SUCCEEDED) con la gravedad EX_INFO y un código de retorno correcto.  
  
 En caso de **error**, sp_rda_test_connection devuelve el error 14856 (STRETCH_MAJOR, STRETCH_CONNECTION_TEST_PROC_FAILED) con la gravedad EX_USER y un código de retorno de error.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|link_state|int|Uno de los valores siguientes, que corresponden a los valores de **link_state_desc**.<br /><br /> -0<br />-1<br />-2<br />-3<br />-4|  
|link_state_desc|varchar(32)|Uno de los valores siguientes, que corresponden a los valores anteriores para **link_state**.<br /><br /> -CORRECTO<br />     El estado entre SQL Server y el servidor remoto de Azure es correcto.<br />-ERROR_AZURE_FIREWALL<br />     El Firewall de Azure impide el vínculo entre SQL Server y el servidor remoto de Azure.<br />-ERROR_NO_CONNECTION<br />     SQL Server no puede establecer una conexión con el servidor remoto de Azure.<br />-ERROR_AUTH_FAILURE<br />     Un error de autenticación impide el vínculo entre SQL Server y el servidor remoto de Azure.<br />-ERROR<br />     Un error que no es un problema de autenticación, un problema de conectividad o un problema de Firewall impide el vínculo entre SQL Server y el servidor remoto de Azure.|  
|error_number|int|Número del error. Si no hay ningún error, este campo es NULL.|  
|error_message|nvarchar(1024)|El mensaje de error. Si no hay ningún error, este campo es NULL.|  
  
## <a name="permissions"></a>Permisos  
 Requiere permisos de db_owner.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="check-the-connection-from-sql-server-to-the-remote-azure-server"></a>Compruebe la conexión desde SQL Server al servidor remoto de Azure.  
  
```sql  
EXECUTE sys.sp_rda_test_connection @database_name = N'<Stretch-enabled database>'  
GO  
  
```  
  
 Los resultados muestran que SQL Server no se puede conectar al servidor remoto de Azure.  
  
|link_state|link_state_desc|error_number|error_message|  
|-----------------|-----------------------|-------------------|--------------------|  
|2|ERROR_NO_CONNECTION|*\<número de error relacionado con la conexión>*|*\<mensaje de error relacionado con la conexión>*|  
  
### <a name="check-the-azure-firewall"></a>Comprobar el Firewall de Azure  
  
```sql  
USE <Stretch-enabled database>  
GO  
EXECUTE sys.sp_rda_test_connection  
GO  
  
```  
  
 Los resultados muestran que el Firewall de Azure impide el vínculo entre SQL Server y el servidor remoto de Azure.  
  
|link_state|link_state_desc|error_number|error_message|  
|-----------------|-----------------------|-------------------|--------------------|  
|1|ERROR_AZURE_FIREWALL|*\<número de error relacionado con el Firewall>*|*\<mensaje de error relacionado con firewall>*|  
  
### <a name="check-authentication-credentials"></a>Comprobar las credenciales de autenticación  
  
```sql  
USE <Stretch-enabled database>  
GO  
EXECUTE sys.sp_rda_test_connection  
GO  
  
```  
  
 Los resultados muestran que un error de autenticación impide el vínculo entre SQL Server y el servidor remoto de Azure.  
  
|link_state|link_state_desc|error_number|error_message|  
|-----------------|-----------------------|-------------------|--------------------|  
|3|ERROR_AUTH_FAILURE|*\<número de error relacionado con la autenticación>*|*\<mensaje de error relacionado con la autenticación>*|  
  
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
  
 Los resultados muestran que la conexión es correcta y que puede habilitar Stretch Database para la base de datos especificada.  
  
|link_state|link_state_desc|error_number|error_message|  
|-----------------|-----------------------|-------------------|--------------------|  
|0|HEALTHY|NULL|NULL|  
  
  
