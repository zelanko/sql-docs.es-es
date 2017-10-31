---
title: TDE para Azure SQL Database y Data Warehouse | Microsoft Docs
description: "Información general del Cifrado de datos transparente para SQL Database y Data Warehouse. En el documento se describen sus ventajas y las opciones de configuración, como Bring Your Own Key y el TDE administrado por un servicio."
keywords: 
services: sql-database
documentationcenter: 
author: becczhang
manager: cguyer
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: security
ms.workload: On Demand
ms.tgt_pltfrm: 
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: rebeccaz
ms.translationtype: HT
ms.sourcegitcommit: 46b16dcf147dbd863eec0330e87511b4ced6c4ce
ms.openlocfilehash: 35c94a39989fda76ea023588b2d7a3aa4e463262
ms.contentlocale: es-es
ms.lasthandoff: 09/05/2017

---


# <a name="transparent-data-encryption-for-azure-sql-database-and-data-warehouse"></a>Cifrado de datos transparente para Azure SQL Database y Data Warehouse

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

El Cifrado de datos transparente (TDE) permite proteger Azure SQL Database y Data Warehouse frente a amenazas de actividad malintencionada mediante llevando a cabo un cifrado y descifrado de la base de datos en tiempo real, copias de seguridad asociadas y archivos de registro de transacciones en reposo sin necesidad de efectuar cambios en la aplicación.

El TDE cifra el almacenamiento de una base de datos completa usando una clave simétrica denominada "clave de cifrado de base de datos" (DEK). Esta clave de cifrado de base de datos está protegida por el protector del TDE, que puede ser un certificado administrado por un servicio ("TDE administrado por un servicio") o una clave asimétrica almacenada en Azure Key Vault ("Bring Your Own Key"). El protector del TDE se establece en el nivel del servidor. 

Durante el inicio de la base de datos se descifra la DEK cifrada y luego se usa para descifrar y volver a cifrar los archivos de base de datos en el proceso del Motor SQL. El TDE efectúa el cifrado y descifrado de E/S en tiempo real de los datos en el nivel de página. Todas las páginas se descifran cuando se leen en la memoria y se cifran antes de escribirse en el disco. Para obtener una descripción general del TDE, vea [Cifrado de datos transparente (TDE)](transparent-data-encryption.md).

SQL Server ejecutado en una máquina virtual de Azure también puede usar una clave asimétrica de Key Vault. Los pasos de configuración son diferentes si se usa una clave asimétrica en Azure SQL Database. Para más información, vea [Administración extensible de claves con el Almacén de claves de Azure (SQL Server)](extensible-key-management-using-azure-key-vault-sql-server.md).

## <a name="service-managed-tde"></a>TDE administrado por un servicio

En Azure, la configuración predeterminada para el TDE es que la clave de cifrado de base de datos está protegida por un certificado de servidor integrado. El certificado de servidor integrado es único para cada servidor. Si hay una base de datos que está en una relación de replicación geográfica, tanto la base de datos principal como la base de datos geográfica secundaria estarán protegidas por la clave de servidor principal de la base de datos principal. Si hay 2 bases de datos conectadas al mismo servidor, comparten el mismo certificado integrado. Microsoft gira automáticamente estos certificados al menos cada 90 días.

Microsoft también mueve y administra sin problemas las claves según sea necesario para la replicación geográfica y las restauraciones. 

> [!IMPORTANT]
> Todas las bases de datos SQL recién creadas se cifran de forma predeterminada mediante el TDE administrado por un servicio. Las bases de datos existentes antes de mayo de 2017 y las bases de datos creadas mediante restauración, replicación geográfica y copia de base de datos no se cifran de forma predeterminada.
>

## <a name="bring-your-own-key"></a>Bring Your Own Key

La compatibilidad de Bring Your Own Key (BYOK) permite al usuario tomar el control de sus claves de cifrado del TDE y controlar quién y cuándo puede tener acceso a ellas. Azure Key Vault (AKV), el sistema de administración de claves externas basado en la nube de Azure, es el primer servicio de administración de claves con el que se ha integrado el TDE para la compatibilidad con BYOK. Con BYOK, la clave de cifrado de base de datos está protegida por una clave asimétrica almacenada en AKV. La clave asimétrica nunca sale de Key Vault. Cuando el servidor tiene los permisos de un almacén de claves, el servidor le envía solicitudes básicas de operación de claves mediante el servicio de Key Vault. La clave asimétrica se establece en el nivel del servidor y la heredan todas las bases de datos de ese servidor. Gracias a la compatibilidad con BYOK, los usuarios ahora pueden controlar las tareas de administración de claves, como las rotaciones de claves, los permisos del almacén de claves, la eliminación de claves y la habilitación de auditorías o de generación de informes en todas las claves de cifrado. Key Vault ofrece una administración central de claves, aprovecha los módulos de seguridad de hardware (HSM) muy supervisados y promueve la separación de la administración de claves y de datos para poder cumplir las normativas. Para obtener más información sobre Key Vault, visite la [página de documentación de Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault).

Para obtener más información sobre el TDE con compatibilidad para BYOK para Azure SQL Database y Data Warehouse, vea [Transparent Data Encryption with Bring Your Own Key support](transparent-data-encryption-byok-azure-sql.md) (Cifrado de datos transparente con compatibilidad para Bring Your Own Key).

Para empezar a usar el TDE con compatibilidad para BYOK, visite la guía de procedimientos [PowerShell: Habilitar el Cifrado de datos transparente con su propia clave desde Azure Key Vault](transparent-data-encryption-byok-azure-sql-configure.md).

## <a name="moving-a-tde-protected-database"></a>Mover una base de datos protegida por el TDE

No es necesario descifrar las bases de datos para las operaciones dentro de Azure. La configuración de TDE en la base de datos de origen o la base de datos principal se hereda de forma transparente en el destino. Aquí se incluyen operaciones que implican:
- Geo-restore
- Restauración a un momento dado de autoservicio
- Restaurar una base de datos eliminada
- Replicación geográfica activa
- Creación de una copia de la base de datos

Al exportar una base de datos protegida por el TDE, no se cifra el contenido exportado de la base de datos. Este contenido exportado se almacena en archivos BACPAC no cifrados. Asegúrese de proteger adecuadamente los archivos BACPAC y de habilitar el TDE una vez completada la importación de la nueva base de datos.

Por ejemplo, si el archivo BACPAC se exporta desde un servidor local de SQL Server, el contenido importado de la base de datos nueva no se cifrará automáticamente. Del mismo modo, si el archivo BACPAC se exporta a un servidor local de SQL Server, la base de datos nueva tampoco se cifrará automáticamente.

La única excepción es cuando se exporta a y desde Azure SQL Database. El TDE se habilita en la nueva base de datos, pero el propio archivo PACPAC sigue sin estar cifrado.

## <a name="managing-transparent-data-encryption-in-the-azure-portal"></a>Administrar el Cifrado de datos transparente en Azure Portal

Para configurar el TDE mediante Azure Portal, debe estar conectado como propietario de Azure, colaborador o administrador de seguridad de SQL. 

El Cifrado de datos transparente se establece en el nivel de la base de datos. Para habilitar el TDE en una base de datos, visite [Azure Portal](https://portal.azure.com) e inicie sesión con su cuenta de administrador o colaborador de Azure. Busque la configuración del TDE en la base de datos de usuario. De forma predeterminada se usa el TDE administrado por un servicio y se genera automáticamente un certificado del TDE para el servidor que contiene la base de datos. 

![TDE administrado por un servicio](./media/transparent-data-encryption-azure-sql/service-managed-tde.png)  

La clave maestra del TDE, también denominada *protector del TDE*, se establece en el nivel del servidor. Para usar el TDE con compatibilidad para Bring Your Own Key y proteger las bases de datos con una clave de Azure Key Vault, consulte la configuración del TDE de su servidor. 

![TDE con compatibilidad para BYOK](./media/transparent-data-encryption-azure-sql/tde-byok-support.png) 

## <a name="managing-transparent-data-encryption-using-powershell"></a>Administrar el Cifrado de datos transparente con PowerShell

Para configurar el TDE mediante PowerShell, debe estar conectado como propietario de Azure, colaborador o administrador de seguridad de SQL. 

| Cmdlet | Description |
| --- | --- |
| [Set-AzureRmSqlDatabaseTransparentDataEncryption](/powershell/module/azurerm.sql/set-azurermsqldatabasetransparentdataencryption) |Habilita o deshabilita el TDE para una base de datos.|
| [Get-AzureRmSqlDatabaseTransparentDataEncryption](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryption) |Obtiene el estado del TDE para una base de datos. |
| [Get-AzureRmSqlDatabaseTransparentDataEncryptionActivity](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryptionactivity) |Comprueba el progreso de cifrado de una base de datos. |
| [Add-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/add-azurermsqlserverkeyvaultkey) |Agrega una clave de Key Vault a un servidor de SQL Server. |
| [Get-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey) |Obtiene las claves de Key Vault de un servidor de SQL Server. |
| [Set-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector) |Establece el protector del TDE para un servidor de SQL Server. |
| [Get-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/get-azurermsqlservertransparentdataencryptionprotector) |Obtiene el protector del Cifrado de datos transparente (TDE). |
| [Remove-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/remove-azurermsqlserverkeyvaultkey) |Quita una clave de Key Vault de un servidor de SQL Server. |
|  | |

## <a name="managing-transparent-data-encryption-using-transact-sql"></a>Administrar el Cifrado de datos transparente con Transact-SQL

Conéctese a la base de datos mediante un inicio de sesión de administrador o de miembro del rol **dbmanager** de la base de datos maestra.

| Command | Description |
| --- | --- |
| [ALTER DATABASE (Azure SQL Database)](/sql/t-sql/statements/alter-database-azure-sql-database) | Use SET ENCRYPTION ON/OFF para cifrar o descifrar una base de datos. |
| [sys.dm_database_encryption_keys](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql) |Devuelve información sobre el estado de cifrado de una base de datos y sus claves de cifrado de la base de datos asociadas. |
| [sys.dm_pdw_nodes_database_encryption_keys](https://docs.microsoft.com/en-us/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-database-encryption-keys-transact-sql) |Devuelve información sobre el estado de cifrado de todos los nodos del almacén de datos y de sus claves de cifrado de base de datos asociadas. | 
|  | |

El protector del TDE no se puede cambiar a una clave de Azure Key Vault mediante Transact-SQL. Debe usar PowerShell o Azure Portal.

## <a name="managing-transparent-data-encryption-using-rest-api"></a>Administrar el Cifrado de datos transparente con una API de REST
 
Para configurar el TDE mediante una API de REST, debe estar conectado como propietario de Azure, colaborador o administrador de seguridad de SQL. 

| Command | Description |
| --- | --- |
|[Crear o actualizar el servidor](/rest/api/sql/servers/createorupdate)|Agrega una identidad de AAD a un servidor de SQL Server (que se usa para conceder acceso a Key Vault).|
|[Crear o actualizar la clave del servidor](/rest/api/sql/serverkeys/createorupdate)|Agrega una clave de Key Vault a un servidor de SQL Server.|
|[Eliminar la clave del servidor](/rest/api/sql/serverkeys/delete)|Quita una clave de Key Vault de un servidor de SQL Server.|
|[Obtener las claves del servidor](/rest/api/sql/serverkeys/get)|Obtiene una clave específica de Key Vault de un servidor de SQL Server.|
|[Mostrar las claves del servidor por servidor](/rest/api/sql/serverkeys/listbyserver)|Obtiene las claves de Key Vault de un servidor de SQL Server.|
|[Crear o actualizar el protector de cifrado](/rest/api/sql/encryptionprotectors/createorupdate)|Establece el protector del TDE para un servidor de SQL Server.|
|[Obtener un protector de cifrado](/rest/api/sql/encryptionprotectors/get)|Obtiene el protector del TDE para un servidor de SQL Server.|
|[Mostrar los protectores de cifrado por servidor](/rest/api/sql/encryptionprotectors/listbyserver)|Obtiene los protectores del TDE de un servidor de SQL Server.|
|[Crear o actualizar la configuración del Cifrado de datos transparente](/rest/api/sql/transparentdataencryptions/createorupdate)|Habilita o deshabilita el TDE para una base de datos.|
|[Obtener la configuración del Cifrado de datos transparente](/rest/api/sql/transparentdataencryptions/get)|Obtiene la configuración del TDE para una base de datos.|
|[Mostrar los resultados de la configuración del Cifrado de datos transparente](/rest/api/sql/transparentdataencryptionactivities/ListByConfiguration)|Obtiene el resultado de cifrado para una base de datos.|

## <a name="next-steps"></a>Pasos siguientes

- Para obtener una descripción general del TDE, vea [Cifrado de datos transparente (TDE)](transparent-data-encryption.md).

- Para obtener más información sobre el TDE con compatibilidad para BYOK para Azure SQL Database y Data Warehouse, visite [Transparent Data Encryption with Bring Your Own Key support](transparent-data-encryption-byok-azure-sql.md) (Cifrado de datos transparente con compatibilidad para Bring Your Own Key).

- Para empezar a usar el TDE con compatibilidad para BYOK, visite la guía de procedimientos [PowerShell: Habilitar el Cifrado de datos transparente con su propia clave desde Azure Key Vault](transparent-data-encryption-byok-azure-sql-configure.md).

- Para más información sobre Key Vault, vea la [página de documentación de Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault).

