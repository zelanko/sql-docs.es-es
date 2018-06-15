---
title: sp_adddistributiondb (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 04/30/2018
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_adddistributiondb_TSQL
- sp_adddistributiondb
helpviewer_keywords:
- sp_adddistributiondb
ms.assetid: e9bad56c-d2b3-44ba-a4d7-ff2fd842e32d
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 7c542df69b94ae6022b8914b050f97d4295e6df5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32992502"
---
# <a name="spadddistributiondb-transact-sql"></a>sp_adddistributiondb (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea una nueva base de datos de distribución e instala el esquema del distribuidor. La base de datos de distribución almacena los procedimientos, esquema y metadatos utilizados en la replicación. Este procedimiento almacenado se ejecuta en el distribuidor de la base de datos maestra con el fin de crear la base de datos de distribución e instalar las tablas y procedimientos almacenados necesarios para habilitar la distribución de replicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_adddistributiondb [ @database= ] 'database'   
    [ , [ @data_folder= ] 'data_folder' ]   
    [ , [ @data_file= ] 'data_file' ]   
    [ , [ @data_file_size= ] data_file_size ]   
    [ , [ @log_folder= ] 'log_folder' ]   
    [ , [ @log_file= ] 'log_file' ]   
    [ , [ @log_file_size= ] log_file_size ]   
    [ , [ @min_distretention= ] min_distretention ]   
    [ , [ @max_distretention= ] max_distretention ]   
    [ , [ @history_retention= ] history_retention ]   
    [ , [ @security_mode= ] security_mode ]   
    [ , [ @login= ] 'login' ]   
    [ , [ @password= ] 'password' ]   
    [ , [ @createmode= ] createmode ]  
    [ , [ @from_scripting = ] from_scripting ] 
    [ , [ @deletebatchsize_xact = ] deletebatchsize_xact ] 
    [ , [ @deletebatchsize_cmd = ] deletebatchsize_cmd ] 
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@database=**] *base de datos '*  
 Es el nombre de la base de datos de distribución que se va a crear. *base de datos* es **sysname**, no tiene ningún valor predeterminado. Si la base de datos especificada ya existe y no está ya marcada como base de datos de distribución, entonces los objetos necesarios para habilitar la distribución están instalados y la base de datos está marcada como base de datos de distribución. Si la base de datos especificada ya está habilitada como base de datos de distribución, se obtiene un error.  
  
 [  **@data_folder=**] **' *** data_folder'*  
 Es el nombre del directorio usado para almacenar el archivo de datos de la base de datos de distribución. *data_folder* es **nvarchar (255)**, su valor predeterminado es null. Si es NULL, se utiliza el directorio de datos para esa instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (por ejemplo, `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data`).  
  
 [  **@data_file=**] **'***data_file***'**  
 Es el nombre del archivo de base de datos. *data_file* es **nvarchar (255)**, su valor predeterminado es **base de datos**. Si es NULL, el procedimiento almacenado crea un nombre de archivo que utiliza el nombre de la base de datos.  
  
 [  **@data_file_size=**] *data_file_size*  
 Es el tamaño inicial del archivo de datos en megabytes (MB). *data_file_size*s **int**, su valor predeterminado es 5 MB.  
  
 [  **@log_folder=**] **'***log_folder***'**  
 Es el nombre del directorio del archivo de registro de la base de datos. *log_folder* es **nvarchar (255)**, su valor predeterminado es null. Si es NULL, se utiliza el directorio de datos para esa instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (por ejemplo, `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data`).  
  
 [  **@log_file=**] **'***ArchivoDeRegistro***'**  
 Es el nombre del archivo de registro. *ArchivoDeRegistro* es **nvarchar (255)**, su valor predeterminado es null. Si es NULL, el procedimiento almacenado crea un nombre de archivo que utiliza el nombre de la base de datos.  
  
 [  **@log_file_size=**] *log_file_size*  
 Es el tamaño inicial del archivo de registro en megabytes (MB). *log_file_size* es **int**, su valor predeterminado es 0 MB, lo que significa que el tamaño del archivo se crea mediante el registro más pequeño archivo tamaño permitido por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [  **@min_distretention=**] *min_distretention*  
 Es el período de retención mínimo, en horas, antes de que las transacciones se eliminen de la base de datos de distribución. *min_distretention* es **int**, su valor predeterminado es 0 horas.  
  
 [  **@max_distretention=**] *max_distretention*  
 Es el período máximo de retención, en horas, antes de que se eliminen las transacciones. *max_distretention* es **int**, con un valor predeterminado de 72 horas. Las suscripciones que no han recibido comandos replicados más antiguos que el período máximo de retención de la distribución se marcarán como inactivas y tendrán que reinicializarse. Se emite RAISERROR 21011 por cada suscripción inactiva. Un valor de **0** significa que las transacciones replicadas no se almacena en la base de datos de distribución.  
  
 [  **@history_retention=**] *history_retention*  
 Es el número de horas que se mantiene el historial. *history_retention* es **int**, su valor predeterminado es 48 horas.  
  
 [  **@security_mode=**] *security_mode*  
 Es el modo de seguridad que se debe utilizar al conectarse con el distribuidor. *security_mode* es **int**, su valor predeterminado es 1. **0** especifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación; **1** especifica la autenticación integrada de Windows.  
  
 [  **@login=**] **'***inicio de sesión***'**  
 Es el nombre de inicio de sesión utilizado al conectarse al distribuidor para crear la base de datos de distribución. Esto es necesario si *security_mode* está establecido en **0**. *login* es de tipo **sysname** y su valor predeterminado es NULL.  
  
 [  **@password=**] **'***contraseña***'**  
 Es la contraseña utilizada para conectarse al distribuidor. Esto es necesario si *security_mode* está establecido en **0**. *contraseña* es **sysname**, su valor predeterminado es null.  
  
 [  **@createmode=**] *createmode*  
 *createmode* es **int**, su valor predeterminado es 1, y puede tener uno de los siguientes valores.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**0**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**1** (predeterminado)|Usar existente o crear base de datos de base de datos y, a continuación, aplicar **instdist.sql** archivo para crear objetos de replicación en la base de datos de distribución.|  
|**2**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
 [  **@from_scripting =** ] *from_scripting*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
 
 [  **@deletebatchsize_xact=**] *deletebatchsize_xact*  
 Especifica el tamaño del lote que se usará durante la limpieza de transacciones expiradas de las tablas de MSRepl_Transactions. *deletebatchsize_xact* es **int**, con un valor predeterminado es 5000. En primer lugar, este parámetro se introdujo en SQL Server 2017, seguido de las versiones de SQL Server 2012 SP4 y el Service Pack 2 de SQL Server 2016.  

 [  **@deletebatchsize_cmd=**] *deletebatchsize_cmd*  
 Especifica el tamaño del lote que se usarán durante la limpieza de comandos expiradas de las tablas MSRepl_Commands. *deletebatchsize_cmd* es **int**, su valor predeterminado es 2000. En primer lugar, este parámetro se introdujo en SQL Server 2017, seguido de las versiones de SQL Server 2012 SP4 y el Service Pack 2 de SQL Server 2016. 
 
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_adddistributiondb** se utiliza en todos los tipos de replicación. Sin embargo, este procedimiento almacenado se ejecuta únicamente en un distribuidor.  
  
 Debe configurar el distribuidor mediante la ejecución de [sp_adddistributor](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md) antes de ejecutar **sp_adddistributiondb**.  
  
 Ejecutar **sp_adddistributor** antes de ejecutar **sp_adddistributiondb**.  
  
## <a name="example"></a>Ejemplo  
  
```  
-- This script uses sqlcmd scripting variables. They are in the form  
-- $(MyVariable). For information about how to use scripting variables    
-- on the command line and in SQL Server Management Studio, see the   
-- "Executing Replication Scripts" section in the topic  
-- "Programming Replication Using System Stored Procedures".  
  
-- Install the Distributor and the distribution database.  
DECLARE @distributor AS sysname;  
DECLARE @distributionDB AS sysname;  
DECLARE @publisher AS sysname;  
DECLARE @directory AS nvarchar(500);  
DECLARE @publicationDB AS sysname;  
-- Specify the Distributor name.  
SET @distributor = $(DistPubServer);  
-- Specify the distribution database.  
SET @distributionDB = N'distribution';  
-- Specify the Publisher name.  
SET @publisher = $(DistPubServer);  
-- Specify the replication working directory.  
SET @directory = N'\\' + $(DistPubServer) + '\repldata';  
-- Specify the publication database.  
SET @publicationDB = N'AdventureWorks2012';   
  
-- Install the server MYDISTPUB as a Distributor using the defaults,  
-- including autogenerating the distributor password.  
USE master  
EXEC sp_adddistributor @distributor = @distributor;  
  
-- Create a new distribution database using the defaults, including  
-- using Windows Authentication.  
USE master  
EXEC sp_adddistributiondb @database = @distributionDB,   
    @security_mode = 1;  
GO  
  
-- Create a Publisher and enable AdventureWorks2012 for replication.  
-- Add MYDISTPUB as a publisher with MYDISTPUB as a local distributor  
-- and use Windows Authentication.  
DECLARE @distributionDB AS sysname;  
DECLARE @publisher AS sysname;  
-- Specify the distribution database.  
SET @distributionDB = N'distribution';  
-- Specify the Publisher name.  
SET @publisher = $(DistPubServer);  
  
USE [distribution]  
EXEC sp_adddistpublisher @publisher=@publisher,   
    @distribution_db=@distributionDB,   
    @security_mode = 1;  
GO  
  
```  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar **sp_adddistributiondb**.  
  
## <a name="see-also"></a>Vea también  
 [Configurar la publicación y la distribución](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [sp_changedistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistributiondb-transact-sql.md)   
 [sp_dropdistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql.md)   
 [sp_helpdistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Configurar la distribución](../../relational-databases/replication/configure-distribution.md)  
  
  
