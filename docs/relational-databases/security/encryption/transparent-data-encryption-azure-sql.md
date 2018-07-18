---
title: Cifrado de datos transparente para Azure SQL Database y Data Warehouse | Microsoft Docs
description: Información general sobre el cifrado de datos transparente para SQL Database y Data Warehouse. En este documento se explican sus ventajas y las opciones de configuración, que incluyen el cifrado de datos transparente administrado por un servicio y el tipo Bring Your Own Key.
keywords: ''
author: becczhang
manager: craigg
editor: ''
ms.prod: ''
ms.reviewer: ''
ms.suite: sql
ms.prod_service: sql-database, sql-data-warehouse
ms.service: sql-database
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.date: 07/09/2018
ms.author: aliceku
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 49a3745e67a51ee8f5eb9625d518328f61593514
ms.sourcegitcommit: dcd29cd2d358bef95652db71f180d2a31ed5886b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2018
ms.locfileid: "37934857"
---
# <a name="transparent-data-encryption-for-sql-database-and-data-warehouse"></a>Cifrado de datos transparente para SQL Database y Data Warehouse
[!INCLUDE[appliesto-xx-asdb-asdw-xxx-md](../../../includes/appliesto-xx-asdb-asdw-xxx-md.md)]

El cifrado de datos transparente (TDE) ayuda a proteger Azure SQL Database y Azure Data Warehouse ante la amenaza de actividad maliciosa. Permite cifrar y descifrar la base de datos en tiempo real, las copias de seguridad asociadas y los archivos de registro de transacciones en reposo sin necesidad de efectuar cambios en la aplicación. De manera predeterminada, TDE está habilitado para todas las instancias de Azure SQL Database recién implementadas. TDE no se puede usar para cifrar la base de datos **maestra** lógica en SQL Database.  La base de datos **maestra** contiene objetos que se necesitan para realizar las operaciones de TDE en las bases de datos de los usuarios.

TDE tendrá que habilitarse manualmente para las bases de datos anteriores o Azure SQL Data Warehouse.  

El cifrado de datos transparente cifra el almacenamiento de una base de datos completa usando una clave simétrica denominada clave de cifrado de base de datos. El protector del cifrado de datos transparente es el encargado de proteger la clave de cifrado de la base de datos. El protector puede ser tanto un certificado administrado por un servicio (cifrado de datos transparente administrado por un servicio) o una clave asimétrica almacenada en Azure Key Vault (Bring Your Own Key). Puede establecer el protector del cifrado de datos transparente en el nivel de servidor. 

Durante el inicio de la base de datos se descifra la clave de cifrado de base de datos cifrada y, luego, se usa para descifrar y volver a cifrar los archivos de base de datos en el proceso del Motor de base de datos de SQL Server. El cifrado de datos transparente realiza el cifrado y descifrado de E/S en tiempo real de los datos en el nivel de página. Todas las páginas se descifran cuando se leen en la memoria y se cifran antes de escribirse en el disco. Para obtener una descripción general del cifrado de datos transparente, vea [Cifrado de datos transparente](transparent-data-encryption.md).

SQL Server ejecutado en una máquina virtual de Azure también puede usar una clave asimétrica de Key Vault. Los pasos de configuración son diferentes si se usa una clave asimétrica en SQL Database. Para obtener más información, vea [Administración extensible de claves con el Almacén de claves de Azure (SQL Server)](extensible-key-management-using-azure-key-vault-sql-server.md).

## <a name="service-managed-transparent-data-encryption"></a>Cifrado de datos transparente administrado por un servicio

En Azure, la configuración predeterminada para el cifrado de datos transparente es que la clave de cifrado de base de datos esté protegida por un certificado de servidor integrado. El certificado de servidor integrado es único para cada servidor. Si hay una base de datos que está en una relación de replicación geográfica, tanto la base de datos principal como la base de datos geográfica secundaria estarán protegidas por la clave de servidor principal de la base de datos principal. Si hay dos bases de datos conectadas al mismo servidor, compartirán el mismo certificado integrado. Microsoft gira automáticamente estos certificados al menos cada 90 días.

Microsoft también mueve y administra sin problemas las claves según sea necesario para la replicación geográfica y las restauraciones. 

> [!IMPORTANT]
> Todas las bases de datos SQL recién creadas se cifran de forma predeterminada mediante el cifrado de datos transparente administrado por un servicio. Las bases de datos existentes antes de mayo de 2017 y las bases de datos creadas mediante restauración, replicación geográfica y copia de base de datos no se cifran de forma predeterminada.
>

## <a name="bring-your-own-key"></a>Bring Your Own Key

Gracias a la compatibilidad con Bring Your Own Key podrá tomar el control de sus claves de cifrado de datos transparente y supervisar quién y cuándo puede tener acceso a ellas. Key Vault, el sistema de administración de claves externas basado en la nube de Azure, es el primer servicio de administración de claves con el que se ha integrado el cifrado de datos transparente para la compatibilidad con Bring Your Own Key. Con Bring Your Own Key, la clave de cifrado de base de datos está protegida por una clave asimétrica almacenada en Key Vault. La clave asimétrica no puede extraerse de Key Vault. Una vez que el servidor tiene los permisos de un almacén de claves, el servidor le envía solicitudes básicas de operación de claves mediante Key Vault. El usuario establece la clave asimétrica en el nivel de servidor y todas las bases de datos de ese servidor la heredan.

Gracias a la compatibilidad con Bring Your Own Key, ahora puede controlar las tareas de administración de claves, como las rotaciones de claves y los permisos del almacén de claves. También puede eliminar claves y habilitar la creación de informes y auditorías en todas las claves de cifrado. Key Vault proporciona una administración de claves centralizada y usa módulos de seguridad de hardware extremadamente supervisados. Key Vault promueve la separación de la administración de claves y datos para ayudarle a satisfacer las normas de cumplimiento. Para obtener más información sobre Key Vault, vea la [página de documentación de Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault).

Para obtener más información sobre el cifrado de datos transparente con compatibilidad con Bring Your Own Key para SQL Database y Data Warehouse, vea [Cifrado de datos transparente con compatibilidad con Bring Your Own Key](transparent-data-encryption-byok-azure-sql.md).

Para empezar a usar el cifrado de datos transparente con compatibilidad con Bring Your Own Device, vea la guía de procedimientos [PowerShell: Habilitar el Cifrado de datos transparente con su propia clave desde Azure Key Vault](transparent-data-encryption-byok-azure-sql-configure.md).

## <a name="move-a-transparent-data-encryption-protected-database"></a>Mover una base de datos protegida por cifrado de datos transparente

No es necesario descifrar las bases de datos para las operaciones dentro de Azure. La configuración del cifrado de datos transparente en la base de datos de origen o la base de datos principal se hereda de forma transparente en el destino. Las operaciones que se incluyen están relacionadas con los siguientes procedimientos:
- Restauración geográfica
- Restauración a un momento dado de autoservicio
- Restauración de una base de datos eliminada
- Replicación geográfica activa
- Creación de una copia de la base de datos

Al exportar una base de datos protegida por cifrado de datos transparente, el contenido exportado de la base de datos no está cifrado. Este contenido exportado se almacena en archivos BACPAC no cifrados. Asegúrese de proteger adecuadamente los archivos BACPAC y habilitar el cifrado de datos transparente cuando haya finalizado la importación de la nueva base de datos.

Por ejemplo, si el archivo BACPAC se exporta desde una instancia local de SQL Server, el contenido importado de la base de datos nueva no se cifrará automáticamente. Del mismo modo, si el archivo BACPAC se exporta a una instancia local de SQL Server, la base de datos nueva tampoco se cifrará automáticamente.

La única excepción es cuando realiza la exportación a y de una base de datos SQL. El cifrado de datos transparente se habilita en la base de datos nueva, pero el propio archivo BACPAC sigue sin estar cifrado.

## <a name="manage-transparent-data-encryption-in-the-azure-portal"></a>Administración del cifrado de datos transparente en Azure Portal

Para configurar el cifrado de datos transparente mediante Azure Portal, debe estar conectado como propietario de Azure, colaborador o administrador de seguridad de SQL. 

El usuario establece el cifrado de datos transparente en el nivel de la base de datos. Para habilitar el cifrado de datos transparente en una base de datos, vaya a [Azure Portal](https://portal.azure.com) e inicie sesión con su cuenta de administrador o colaborador de Azure. Busque la configuración de cifrado de datos transparente en la base de datos de usuarios. De manera predeterminada, se usa el cifrado de datos transparente administrado por un servicio. Se genera un certificado de cifrado de datos transparente automáticamente para el servidor en el que se almacena la base de datos. 

![Cifrado de datos transparente administrado por un servicio](./media/transparent-data-encryption-azure-sql/service-managed-tde.png)  

El usuario establece la clave maestra de cifrado de datos transparente, también conocida como protector de cifrado de datos transparente, en el nivel de servidor. Para usar el cifrado de datos transparente con compatibilidad con Bring Your Own Key y proteger las bases de datos con una clave de Key Vault, vea la configuración de cifrado de datos transparente de su servidor. 

![Cifrado de datos transparente con compatibilidad con Bring Your Own Key](./media/transparent-data-encryption-azure-sql/tde-byok-support.png) 

## <a name="manage-transparent-data-encryption-by-using-powershell"></a>Administración del cifrado de datos transparente con PowerShell

Para configurar el cifrado de datos transparente mediante PowerShell, debe estar conectado como propietario de Azure, colaborador o administrador de seguridad de SQL. 

| Cmdlet | Descripción |
| --- | --- |
| [Set-AzureRmSqlDatabaseTransparentDataEncryption](/powershell/module/azurerm.sql/set-azurermsqldatabasetransparentdataencryption) |Habilita o deshabilita el cifrado de datos transparente para una base de datos.|
| [Get-Azure-Rm-Sql-Database-Transparent-Data-Encryption](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryption) |Obtiene el estado de cifrado de datos transparente para una base de datos. |
| [Get-Azure-Rm-Sql-Database-Transparent-Data-Encryption-Activity](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryptionactivity) |Comprueba el progreso de cifrado de una base de datos. |
| [Add-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/add-azurermsqlserverkeyvaultkey) |Agrega una clave de Key Vault a una instancia de SQL Server. |
| [Get-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey) |Obtiene las claves de Key Vault para una instancia de SQL Server.  |
| [Set-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector) |Establece el protector de cifrado de datos transparente para una instancia de SQL Server. |
| [Get-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/get-azurermsqlservertransparentdataencryptionprotector) |Obtiene el protector de cifrado de datos transparente. |
| [Remove-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/remove-azurermsqlserverkeyvaultkey) |Quita una clave de Key Vault de una instancia de SQL Server. |
|  | |

## <a name="manage-transparent-data-encryption-by-using-transact-sql"></a>Administración del cifrado de datos transparente con Transact-SQL

Conéctese a la base de datos mediante un inicio de sesión de administrador o de miembro del rol **dbmanager** de la base de datos maestra.

| Comando | Descripción |
| --- | --- |
| [ALTER DATABASE (Azure SQL Database)](/sql/t-sql/statements/alter-database-azure-sql-database) | SET ENCRYPTION ON/OFF cifra o descifra una base de datos. |
| [sys.dm_database_encryption_keys](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql) |Devuelve información sobre el estado de cifrado de una base de datos y sus claves de cifrado de la base de datos asociadas. |
| [sys.dm_pdw_nodes_database_encryption_keys](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-database-encryption-keys-transact-sql) |Devuelve información sobre el estado de cifrado de todos los nodos del almacén de datos y de sus claves de cifrado de base de datos asociadas. | 
|  | |

No se puede cambiar el protector de cifrado de datos transparente a una clave de Key Vault con Transact-SQL. Use PowerShell o Azure Portal.

## <a name="manage-transparent-data-encryption-by-using-the-rest-api"></a>Administración del cifrado de datos transparente con la API de REST
 
Para configurar el cifrado de datos transparente mediante la API de REST, debe estar conectado como propietario de Azure, colaborador o administrador de seguridad de SQL. 

| Comando | Descripción |
| --- | --- |
|[Crear o actualizar el servidor](/rest/api/sql/servers/createorupdate)|Agrega una identidad de Azure Active Directory a una instancia de SQL Server que se usa para conceder acceso a Key Vault.|
|[Crear o actualizar la clave del servidor](/rest/api/sql/serverkeys/createorupdate)|Agrega una clave de Key Vault a una instancia de SQL Server.|
|[Eliminar la clave del servidor](/rest/api/sql/serverkeys/delete)|Quita una clave de Key Vault de una instancia de SQL Server.|
|[Obtener las claves del servidor](/rest/api/sql/serverkeys/get)|Obtiene una clave específica de Key Vault de una instancia de SQL Server.|
|[Mostrar las claves del servidor por servidor](/rest/api/sql/serverkeys/listbyserver)|Obtiene las claves de Key Vault para una instancia de SQL Server. |
|[Crear o actualizar el protector de cifrado](/rest/api/sql/encryptionprotectors/createorupdate)|Establece el protector de cifrado de datos transparente para una instancia de SQL Server.|
|[Obtener un protector de cifrado](/rest/api/sql/encryptionprotectors/get)|Obtiene el protector de cifrado de datos transparente para una instancia de SQL Server.|
|[Mostrar los protectores de cifrado por servidor](/rest/api/sql/encryptionprotectors/listbyserver)|Obtiene el protector de cifrado de datos transparente para una instancia de SQL Server. |
|[Crear o actualizar la configuración del Cifrado de datos transparente](/rest/api/sql/transparentdataencryptions/createorupdate)|Habilita o deshabilita el cifrado de datos transparente para una base de datos.|
|[Obtener la configuración del Cifrado de datos transparente](/rest/api/sql/transparentdataencryptions/get)|Obtiene la configuración de cifrado de datos transparente para una base de datos.|
|[Mostrar los resultados de la configuración del Cifrado de datos transparente](/rest/api/sql/transparentdataencryptionactivities/ListByConfiguration)|Obtiene el resultado de cifrado para una base de datos.|

## <a name="next-steps"></a>Pasos siguientes

- Para obtener una descripción general del cifrado de datos transparente, vea [Cifrado de datos transparente](transparent-data-encryption.md).
- Para obtener más información sobre el cifrado de datos transparente con compatibilidad con Bring Your Own Key para SQL Database y Data Warehouse, vea [Cifrado de datos transparente con compatibilidad con Bring Your Own Key](transparent-data-encryption-byok-azure-sql.md).
- Para empezar a usar el cifrado de datos transparente con compatibilidad con Bring Your Own Device, vea la guía de procedimientos [PowerShell: Habilitar el Cifrado de datos transparente con su propia clave desde Azure Key Vault](transparent-data-encryption-byok-azure-sql-configure.md).
- Para obtener más información sobre Key Vault, vea la [página de documentación de Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault).
