---
title: TDE - Bring Your Own Key - Azure SQL | Microsoft Docs
description: "Descripción general de la compatibilidad entre Bring Your Own Key y el cifrado de datos transparente (TDE) con Azure Key Vault para SQL Database y SQL Data Warehouse. En este documento se explican las ventajas de la característica y su funcionamiento, así como diversas consideraciones y recomendaciones a tener en cuenta."
keywords: 
services: sql-database
documentationcenter: 
author: becczhang
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom:
- security
ms.workload: 
ms.tgt_pltfrm: 
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: rebeccaz
ms.translationtype: HT
ms.sourcegitcommit: 54e4c8309c290255cb2885fab04bb394bc453046
ms.openlocfilehash: 2950cf2e403cd0afd337c1578d7bbe656f2a6e53
ms.contentlocale: es-es
ms.lasthandoff: 10/16/2017

--- 

# <a name="transparent-data-encryption-with-bring-your-own-key-support-for-azure-sql-database-and-data-warehouse"></a>Cifrado de datos transparente compatible con Bring Your Own Key para Azure SQL Database y SQL Data Warehouse

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

La compatibilidad con Bring Your Own Key (BYOK) del [Cifrado de datos transparente (TDE)](transparent-data-encryption.md) permite al usuario tomar el control de sus claves de cifrado de TDE y supervisar quién y cuándo puede tener acceso a ellas. [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault), el sistema de administración de claves externas basado en la nube de Azure, es el primer servicio de administración de claves en el que TDE ha integrado compatibilidad con BYOK. Con BYOK, la clave de cifrado de base de datos está protegida por una clave asimétrica almacenada en Key Vault. La clave asimétrica se establece en el nivel de servidor y la heredan todas las bases de datos de ese servidor. 

Gracias a la compatibilidad con BYOK, los usuarios pueden controlar las tareas de administración de claves, como las rotaciones de claves, los permisos del almacén de claves, la eliminación de claves y la habilitación de auditorías o informes en todas las claves de cifrado. Key Vault ofrece una administración central de claves, aprovecha los módulos de seguridad de hardware (HSM) muy supervisados y promueve la separación de la administración de claves y de datos para poder cumplir la normativa. 

TDE con BYOK ofrece estas ventajas:
- Mayor transparencia y un control granular con capacidad de administrar automáticamente el protector de TDE   
- Administración central de las claves de cifrado de TDE (junto con otras claves y secretos usados en otros servicios de Azure) hospedándolas en Key Vault
- Separación de la administración de claves y datos dentro de la organización, para admitir la separación de roles
- Mayor nivel de confianza de sus propios clientes, ya que Key Vault está diseñado para que Microsoft no vea ni extraiga ninguna clave de cifrado. 
- Compatibilidad con la rotación de claves

> [!IMPORTANT]
> Para aquellos que usen TDE administrado por el servicio y quieran empezar a usar Key Vault, TDE permanece activado durante el proceso de cambio a una clave en Key Vault. No se produce ningún tiempo de inactividad ni el recifrado de los propios archivos de la base de datos. Al cambiar de una clave administrada por el servicio a una clave de Key Vault, se necesita volver a cifrar la clave de cifrado de la base de datos, lo cual es una operación rápida y en línea.
>

## <a name="how-does-tde-with-byok-support-work"></a>¿Cómo funciona TDE con la compatibilidad con BYOK?
 
![Autenticación del servidor en Key Vault](./media/transparent-data-encryption-byok-azure-sql/tde-byok-server-authentication-flow.PNG)

Cuando TDE está configurado para usar una clave de Key Vault, el servidor envía la clave de cifrado de cada base de datos compatible con TDE a Key Vault para una solicitud de *encapsulado de clave*. Key Vault devuelve la clave de cifrado de la base de datos cifrada, que se almacena en la base de datos de usuario. 

Es importante tener en cuenta que **desde el momento en que una clave se almacena en Key Vault, no abandona nunca ese almacén**. Una clave respaldada por un módulo de seguridad de hardware (HSM) en Key Vault nunca se sale de los límites de seguridad de HSM. El servidor solamente puede enviar solicitudes de operación de la clave al material de clave del protector de TDE en Key Vault. El administrador de Key Vault tiene derecho a revocar cuando quiera los permisos de Key Vault para el servidor, en cuyo caso se cortarán todas las conexiones al servidor. 

## <a name="considerations"></a>Consideraciones

Al usar TDE con BYOK, tiene a su disposición las dos tareas de administración de claves y los costos relacionados de usar el propio almacén de claves. Estas consideraciones se tratan en las dos secciones siguientes.

### <a name="key-management-responsibilities"></a>Responsabilidades de administración de claves

Asumir la administración de claves de cifrado de los recursos de una aplicación es una responsabilidad importante. Al usar TDE con BYOK a través de Key Vault, puede asumir estas tareas de administración de claves:
- **Rotaciones de clave:** los protectores de TDE deben rotar según la normativa interna o los requisitos de cumplimiento. Las rotaciones de clave pueden realizarse a través del almacén de claves del protector de TDE.  
- **Permisos del almacén de claves**: los permisos en Key Vault se aprovisionan en el nivel de un almacén de claves y del servidor. Los permisos del servidor en un almacén de claves se pueden revocar en cualquier momento mediante la directiva de acceso del almacén de claves.
- **Eliminación de claves**: las claves se pueden quitar de Key Vault y el servidor SQL Server por motivos de seguridad adicional o de cumplimiento normativo.
- **Auditoría/Informes en todas las claves de cifrado**: Key Vault proporciona registros que son fáciles de insertar en otras herramientas de administración de eventos e información de seguridad (SIEM). Operations Management Suite (OMS) [Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-key-vault) es un servicio de ejemplo que ya está integrado.

### <a name="pricing-considerations"></a>Precio 

TDE compatible con BYOK es una capacidad de seguridad que está integrada en Azure SQL Database y SQL Data Warehouse sin costo adicional. Sin embargo, el uso de Key Vault sí implica ciertos costos. Las operaciones de Key Vault realizadas por el servidor se cobran como operaciones normales en el almacén y se ajustan a los [precios](https://azure.microsoft.com/pricing/details/key-vault/) de Key Vault. El servidor envía solicitudes a Key Vault para los siguientes eventos:
- Reinicios de instancias de SQL
- Sustituciones de claves
- Comprobación cada 6 horas de si se han realizado cambios en los permisos del servidor al almacén de claves

## <a name="important-warnings"></a>Advertencias importantes

### <a name="loss-of-access-to-keys"></a>Pérdida de acceso a las claves

En cuanto un servidor deja de tener acceso al protector de TDE (ya sea porque se han quitado los permisos de Key Vault o porque se ha eliminado una clave), **se bloquean todas las conexiones a las bases de datos cifradas en el servidor y estas bases de datos se quedan sin conexión y se quitan en un plazo de 24 horas**. Ya no se podrá acceder a las copias de seguridad antiguas que estén cifradas con la clave que no está disponible. Si se produjera un caso extremo donde se sospecha que hay una clave en peligro (por ejemplo, en el que un servicio o un usuario tienen acceso no autorizado a la clave), es mejor eliminar la clave siguiendo las directrices de [Remove a Transparent Data Encryption (TDE) protector using PowerShell](transparent-data-encryption-byok-azure-sql-remove-tde-protector.md) (Eliminación de un protector de Cifrado de datos transparente [TDE] mediante PowerShell). Las bases de datos deben quitarse antes de eliminar un protector de TDE activo para evitar hasta 10 minutos de posible pérdida de datos.  

### <a name="expired-keys"></a>Claves expiradas

Como la disponibilidad del protector de TDE afecta directamente a la disponibilidad de la base de datos, no está permitido agregar una clave con fecha de expiración a un servidor SQL Server. Si ya se usa una clave como un protector de TDE para un servidor y después se agrega una fecha de expiración en Azure Key Vault, **cuando la clave expire, las bases de datos cifradas no podrán acceder más a su protector de TDE y se quitarán en un plazo de 24 horas.**

### <a name="deleted-server-identities"></a>Identidades de servidor eliminadas 

El acceso de un servidor a Key Vault se administra a través de la identidad única de Azure Active Directory (AAD) del servidor. Por lo tanto, si se elimina la identidad del servidor de AAD, el servidor pierde el acceso a sus almacenes de claves. Como resultado, **se bloquean todas las conexiones a las bases de datos cifradas en el servidor y estas bases de datos se quedan sin conexión y se quitan en un plazo de 24 horas.**

## <a name="limitations"></a>Limitaciones

Los almacenes de claves que se usan para TDE deben estar en el mismo inquilino de AAD que el servidor de SQL Database y SQL Data Warehouse. No se admiten interacciones entre el servidor y el almacén de claves de varios inquilinos. Un recurso que se cifra con una clave de Key Vault no se puede cambiar de una suscripción de Azure a otra. Al cambiar el recurso de una suscripción a otra se rompen todos los controles de acceso a Key Vault que posibilitan TDE con BYOK. Si es necesario mover algún recurso a otra suscripción, cambie el modo TDE de BYOK a [TDE administrado por el servicio](transparent-data-encryption-azure-sql.md). 

No se admiten protectores de TDE únicos para una base de datos o un almacén de datos. El protector de TDE se establece en el nivel de servidor y lo heredan todos los recursos del servidor. 

## <a name="guidelines-for-managing-encrypted-databases"></a>Directrices para administrar bases de datos cifradas

### <a name="high-availability-and-disaster-recovery"></a>Alta disponibilidad y recuperación ante desastres
  
Hay dos maneras de configurar la replicación geográfica para servidores mediante Key Vault: 

- **Almacén de claves independiente**: cada servidor tiene acceso a un almacén de claves independiente (lo ideal es que cada uno tenga su propia región de Azure). Esta es la configuración recomendada, puesto que cada servidor tiene su propia copia del protector de TDE para las bases de datos cifradas con replicación geográfica. Si una de las regiones de Azure del servidor se desconecta, los demás servidores pueden seguir teniendo acceso a las bases de datos con replicación geográfica.   

- **Almacén de claves compartido**: todos los servidores comparten el mismo almacén de claves. Esta configuración es más sencilla, pero si se queda sin conexión la región de Azure donde se encuentra el almacén de claves, los servidores no podrán leer las bases de datos cifradas con replicación geográfica ni sus propias bases de datos cifradas. 
 
Para empezar, use el cmdlet [Add-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/add-azurermsqlserverkeyvaultkey) para agregar cada clave de Key Vault del servidor a los otros servidores en el vínculo de replicación geográfica.  
(Ejemplo de un identificador de clave de Key Vault: *https://contosokeyvault.vault.azure.net/keys/Key1/1a1a2b2b3c3c4d4d5e5e6f6f7g7g8h8h*)

   ```powershell
   <# Include the version guid in the KeyId #>
   Add-AzureRmSqlServerKeyVaultKey `
   -KeyId <KeyVaultKeyId> `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName>
   ```

>[!NOTE]
>La combinación de la longitud de caracteres del nombre del almacén de claves y del nombre de la clave no puede superar los 94 caracteres.
>

Siga los pasos de [Introducción: grupos de conmutación por error y replicación geográfica activa](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview) para configurar la replicación geográfica activa con estos servidores y desencadenar una conmutación por error.  

### <a name="backup-and-restore"></a>Copias de seguridad y restauración

Desde el momento en que se cifra una base de datos con TDE mediante una clave de Key Vault, las copias de seguridad que se generan también se cifran con el mismo protector de TDE.

Para restaurar una copia de seguridad cifrada con un protector de TDE de Key Vault, asegúrese de que el material de clave aún está en el almacén original bajo el nombre de clave original. Cuando se cambia el protector de TDE para una base de datos, las copias de seguridad antiguas de la base de datos **no** se actualizan para usar el protector de TDE más reciente. Por tanto, se recomienda mantener todas las versiones antiguas del protector de TDE en Key Vault de modo que se puedan restaurar las copias de seguridad de base de datos. 

Si una clave que podría ser necesaria para restaurar una copia de seguridad ya no se encuentra en su almacén de claves original, se devuelve el siguiente mensaje de error: "Target server <Servername> does not have access to all AKV Uris created between <Timestamp #1> and <Timestamp #2>. Vuelva a intentarlo después de restaurar todos los URI de AKV."

Para mitigarlo, ejecute el cmdlet [Get-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey) para devolver la lista de claves de Key Vault que se agregaron al servidor. Para asegurarse de que se pueden restaurar todas las copias de seguridad, compruebe que el servidor de destino para la copia de seguridad tiene acceso a todas estas claves.

   ```powershell
   Get-AzureRmSqlServerKeyVaultKey `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName>
   ```
Para más información sobre la recuperación de copia de seguridad para SQL Database, vea [Recuperación de una Base de datos SQL de Azure mediante copias de seguridad automatizadas](https://docs.microsoft.com/azure/sql-database/sql-database-recovery-using-backups). Si quiere saber más sobre la recuperación de copias de seguridad para SQL Data Warehouse, vea [Restauración de SQL Data Warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-restore-database-overview).

## <a name="best-practices"></a>Procedimientos recomendados

### <a name="key-management"></a>Administración de claves 

Para garantizar una recuperación rápida de las claves y el acceso a los datos fuera de Azure, recomendamos el siguiente proceso:
- Cree localmente la clave de cifrado en un dispositivo HSM local. (Asegúrese de que se trata de una clave RSA 2048 asimétrica, para que así se pueda almacenar en Azure Key Vault).
- Importe el archivo de clave de cifrado (.pfx, .byok o .backup) a Azure Key Vault. Le recomendamos que use un almacén de claves con [soft-delete](https://docs.microsoft.com/azure/key-vault/key-vault-ovw-soft-delete) habilitado para la protección de la recuperación ante la eliminación accidental de claves.
- Antes de usar la clave por primera vez en Azure Key Vault, cree una copia de seguridad clave de Azure Key Vault. Obtenga más información sobre el comando [Backup-AzureKeyVaultKey](https://msdn.microsoft.com/library/mt126292.aspx) .
- Cada vez que se haga algún cambio en la clave (por ejemplo, que se agregue ACL, etiquetas o atributos clave), asegúrese de crear otra copia de seguridad de la clave de Azure Key Vault.
- Durante una sustitución de claves, **mantenga versiones anteriores de la clave** en el almacén de claves para que se puedan restaurar copias de seguridad de base de datos anteriores. 

Para los escenarios de producción, recomendamos encarecidamente crear primero la clave de cifrado de TDE a nivel local y después importar la clave asimétrica, ya que así el administrador puede custodiar la clave en un sistema de custodia de clave. Si la clave asimétrica se crea en Azure Key Vault, no se puede custodiar porque la clave privada nunca puede abandonar el almacén. Las claves que se usen para proteger datos críticos se deben custodiar. Si se pierde una clave asimétrica, los datos de la clave no podrán recuperarse nunca más.

### <a name="pre-configuration-for-replicated-databases"></a>Configuración previa de bases de datos replicadas

Si se va a replicar una base de datos en otro servidor, asegúrese de que el servidor tiene acceso a una copia del material de clave de Key Vault usado en el otro servidor **antes** de mover o replicar la base de datos.  

Se recomienda que todos los servidores tengan acceso a una copia del material de clave de Key Vault usado en otro servidor, que se almacena en un almacén de claves independiente (lo ideal es que cada uno se almacene en la misma región de Azure que el servidor). Con esta configuración, cada servidor tiene su propia copia del protector de TDE para las bases de datos cifradas con replicación geográfica. Si una de las regiones de Azure del servidor se desconecta, los demás servidores pueden seguir teniendo acceso a las bases de datos replicadas.

## <a name="next-steps"></a>Pasos siguientes

- Primeros pasos con la compatibilidad de Bring Your Own Key para TDE: [PowerShell: Enable Transparent Data Encryption using your own key from Azure Key Vault](transparent-data-encryption-byok-azure-sql-configure.md) (PowerShell: Habilitación del cifrado de datos transparente usando su propia clave de Azure Key Vault).
- Aprenda a rotar el protector de TDE de un servidor para cumplir con los requisitos de seguridad: [Rotate the Transparent Data Encryption (TDE) protector using PowerShell](transparent-data-encryption-byok-azure-sql-key-rotation.md) (Rotación del protector de cifrado de datos transparente mediante PowerShell).
- En caso de riesgo de seguridad, aprenda a quitar un protector de TDE que está potencialmente en peligro: [Remove a Transparent Data Encryption (TDE) protector using PowerShell](transparent-data-encryption-byok-azure-sql-remove-tde-protector.md) (Eliminación de un protector de cifrado de datos transparente [TDE] mediante PowerShell). 

