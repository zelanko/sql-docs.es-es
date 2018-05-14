---
title: TDE - Bring Your Own Key (BYOK) - Azure SQL | Microsoft Docs
description: Compatibilidad entre Bring Your Own Key (BYOK) y el cifrado de datos transparente (TDE) con Azure Key Vault para SQL Database y SQL Data Warehouse. Descripción general, ventajas, cómo funciona, consideraciones y recomendaciones de TDE con BYOK.
keywords: ''
services: sql-database
documentationcenter: ''
author: aliceku
manager: craigg
ms.prod: ''
ms.reviewer: ''
ms.suite: sql
ms.prod_service: sql-database, sql-data-warehouse
ms.service: sql-database
ms.custom: ''
ms.component: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.date: 04/19/2018
ms.author: aliceku
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 2265778ca41dd82a1e55fe01749bd2d5057f5f1c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="transparent-data-encryption-with-bring-your-own-key-support-for-azure-sql-database-and-data-warehouse"></a>Cifrado de datos transparente compatible con Bring Your Own Key para Azure SQL Database y SQL Data Warehouse
[!INCLUDE[appliesto-xx-asdb-asdw-xxx-md](../../../includes/appliesto-xx-asdb-asdw-xxx-md.md)]

La compatibilidad con Bring Your Own Key (BYOK) del [Cifrado de datos transparente (TDE)](transparent-data-encryption.md) permite cifrar la Clave de cifrado de base de datos (DEK) con una clave asimétrica llamada "protector del TDE".  El protector del TDE se almacena bajo su control en [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault), el sistema de administración de claves externas basado en la nube de Azure. Azure Key Vault es el primer servicio de administración de claves en el que TDE ha integrado la compatibilidad con BYOK. El protector del TDE se encarga de cifrar y descifrar la DEK de TDE, que se almacena en la página de arranque de la base de datos. El protector del TDE se almacena en Azure Key Vault y permanece siempre en el almacén de claves. Si se revoca el acceso del servidor al almacén de claves, las bases de datos no se pueden descifrar ni leer en la memoria.  El protector del TDE se establece en el nivel de servidor lógico, y todas las bases de datos asociadas a ese servidor heredan dicha configuración. 

Gracias a la compatibilidad con BYOK, los usuarios pueden controlar las tareas de administración de claves, como las rotaciones de claves, los permisos del almacén de claves, la eliminación de claves y la habilitación de auditorías o informes en todos los protectores del TDE mediante la funcionalidad de Azure Key Vault. Key Vault ofrece una administración central de claves, aprovecha los módulos de seguridad de hardware (HSM) muy supervisados y permite la separación de las tareas entre la administración de claves y los datos para facilitar el cumplimiento normativo.  


TDE con BYOK ofrece estas ventajas:
- Mayor transparencia y un control granular con capacidad de administrar automáticamente el protector de TDE   
- Administración central de los protectores del TDE (junto con otras claves y secretos usados en otros servicios de Azure) hospedándolas en Key Vault
- Separación de las responsabilidades de administración de claves y datos dentro de la organización para facilitar la separación de tareas
- Mayor nivel de confianza de sus propios clientes, ya que Key Vault está diseñado para que Microsoft no vea ni extraiga ninguna clave de cifrado. 
- Compatibilidad con la rotación de claves

> [!IMPORTANT]
> Para aquellos que usen un TDE administrado por el servicio y quieran empezar a usar Key Vault, el TDE permanece habilitado durante el proceso de cambio a un protector del TDE en Key Vault. Los archivos de la base de datos siempre están activos y no es necesario volverlos a cifrar. Al cambiar de una clave administrada por el servicio a una clave de Key Vault, solo se necesita volver a cifrar la clave de cifrado de la base de datos (DEK), lo cual es una operación rápida y en línea. 
>

## <a name="how-does-tde-with-byok-support-work"></a>¿Cómo funciona TDE con la compatibilidad con BYOK?
 
![Autenticación del servidor en Key Vault](./media/transparent-data-encryption-byok-azure-sql/tde-byok-server-authentication-flow.PNG)

Cuando TDE se configura por primera vez para usar un protector del TDE de Key Vault, el servidor envía a Key Vault la DEK de cada base de datos compatible con TDE para una solicitud de encapsulado de clave. Key Vault devuelve la clave de cifrado de la base de datos cifrada, que se almacena en la base de datos de usuario.  

>[!IMPORTANT]
>Es importante tener en cuenta que **una vez que un protector del TDE se almacena en Azure Key Vault, permanece siempre ahí**. El servidor lógico solo puede enviar solicitudes de operación relativas a la clave al material de claves del protector del TDE de Key Vault, y **no accede nunca a dicho protector ni lo almacena en caché**. El administrador de Key Vault tiene derecho a revocar cuando quiera los permisos de Key Vault para el servidor, en cuyo caso se cortarán todas las conexiones a este. 
>


## <a name="guidelines-for-configuring-tde-with-byok"></a>Directrices para configurar TDE con BYOK

### <a name="general-guidelines"></a>Directrices generales
- Asegúrese de que Azure Key Vault y Azure SQL Database vayan a estar en el mismo inquilino.  **No se admiten** interacciones entre el servidor y el almacén de claves de varios inquilinos.
- Decida qué suscripciones se van a usar para los recursos necesarios, ya que para mover el servidor por las suscripciones más adelante se necesitará una nueva configuración de TDE con BYOK.
- Al configurar TDE con BYOK, es importante tener en cuenta la carga depositada en el almacén de claves por las operaciones repetidas de encapsular/desencapsular. Por ejemplo, dado que todas las bases de datos asociadas a un servidor lógico usan el mismo protector de TDE, una conmutación por error de ese servidor desencadenará tantas operaciones de clave en el almacén como bases de datos haya en el servidor. Según nuestra experiencia y los [límites de servicio del almacén de claves](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-service-limits) que hemos documentado, se recomienda asociar como máximo 500 bases de datos estándar o de uso general, o 200 bases de datos premium o críticas para la empresa a un Azure Key Vault en una sola suscripción para garantizar una disponibilidad alta uniforme al acceder al protector de TDE en el almacén. 
- Opción recomendada: Guarde una copia local del protector del TDE.  Para ello es necesario que un dispositivo HSM cree un protector del TDE localmente y que un sistema de custodia de claves almacene una copia local del protector del TDE.


### <a name="guidelines-for-configuring-azure-key-vault"></a>Directrices para configurar Azure Key Vault

- Cree un Key Vault con la opción de [eliminación temporal](https://docs.microsoft.com/azure/key-vault/key-vault-ovw-soft-delete) habilitada para protegerlo de una pérdida de datos en caso de que se eliminen por error una clave o un almacén de claves.  Debe usar [PowerShell para habilitar la propiedad "eliminación temporal"](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-soft-delete-powershell) en Key Vault. Esta opción aún no está disponible desde el portal de Azure Key Vault, pero la requiere SQL:  
  - Los recursos eliminados temporalmente se conservan durante un período de tiempo determinado de 90 días, a menos que se recuperen o purguen.
  - Las acciones de **recuperación** y **purga** tienen permisos propios asociados a una directiva de acceso al almacén de claves. 

- Conceda al servidor lógico acceso al almacén de datos usando su identidad de Azure Active Directory (Azure AD).  Si se usa la IU del portal, la identidad de Azure AD se crea automáticamente y los permisos de acceso al almacén de claves se conceden al servidor.  Al utilizar PowerShell para configurar TDE con BYOK, se debe crear la identidad de Azure AD y comprobar su finalización. Vea [Configuración de TDE con BYOK](transparent-data-encryption-byok-azure-sql-configure.md) para recibir instrucciones paso a paso para usar PowerShell.

  >[!NOTE]
  >Si la identidad de Azure AD **se elimina por error, o bien si se revocan los permisos del servidor** mediante la directiva de acceso al almacén de claves, el servidor perderá acceso al almacén de claves.
  >
  
- Habilite la auditoría y los informes en todas las claves de cifrado: Key Vault proporciona registros que son fáciles de insertar en otras herramientas de administración de eventos e información de seguridad (SIEM). Operations Management Suite (OMS) [Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-key-vault) es un ejemplo de un servicio que ya está integrado.
- Para garantizar una alta disponibilidad de las bases de datos cifradas, configure cada servidor lógico con dos almacenes de Azure Key Vault que se encuentren en regiones distintas.


### <a name="guidelines-for-configuring-the-tde-protector-asymmetric-key-stored-in-azure-key-vault"></a>Directrices para configurar un protector del TDE (clave asimétrica) almacenado en Azure Key Vault

- Cree localmente la clave de cifrado en un dispositivo HSM local. Asegúrese de que se trate de una clave RSA 2048 asimétrica, para que, así, se pueda almacenar en Azure Key Vault.
- Asigne una custodia a la clave en un sistema de custodia de clave.  
- Importe el archivo de clave de cifrado (.pfx, .byok o .backup) a Azure Key Vault. 
    

>[!NOTE] 
    >Si quiere llevar a cabo pruebas, puede crear una clave con Azure Key Vault. Sin embargo, dicha clave no se puede tener en custodia porque la clave privada debe permanecer siempre en el almacén de claves.  En el momento de usar claves para cifrar los datos de producción, es necesario crear una copia de seguridad de estas y asignarles una custodia, ya que la pérdida de una clave (al eliminarla del almacén de claves por error o en caso de que expire) supone una pérdida de datos permanente.
    >
    
- Debe usar una clave sin fecha de expiración, y no puede establecer una fecha de expiración para una clave que ya esté en uso: **una vez que expire la clave, las bases de datos cifradas perderán el acceso a su protector del TDE y se anularán en un plazo de 24 horas**.
- Asegúrese de que la clave esté habilitada y de que tenga permisos para llevar a cabo las operaciones *get*, *wrap key* y *unwrap key*.
- Cree una copia de seguridad de la clave de Azure Key Vault antes de usar la clave en Azure Key Vault por primera vez. Obtenga más información sobre el comando [Backup-AzureKeyVaultKey](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/backup-azurekeyvaultkey?view=azurermps-5.1.1) .
- Cree una nueva copia de seguridad cada vez que se haga algún cambio en la clave (por ejemplo, al agregar ACL, etiquetas o atributos de clave).
- Al rotar las claves, **conserve las versiones anteriores** en el almacén de claves para que se puedan restaurar copias de seguridad de bases de datos anteriores. Cuando se cambia el protector del TDE de una base de datos, las copias de seguridad antiguas de la base de datos **no se actualizan** para usar el protector del TDE más reciente.  Cada una de las copias de seguridad necesita el protector del TDE con el que se creó en el momento de la restauración. Las rotaciones de clave se pueden llevar a cabo siguiendo las instrucciones del artículo [Girar el protector del Cifrado de datos transparente (TDE) mediante PowerShell](transparent-data-encryption-byok-azure-sql-key-rotation.md).
- Conserve todas las claves que haya usado anteriormente en Azure Key Vault después de cambiar a las claves administradas por el servicio.  Con ello se garantiza que se puedan restaurar las copias de seguridad de bases de datos con los protectores del TDE almacenados en Azure Key Vault.  Los protectores del TDE creados con Azure Key Vault deben conservarse hasta que se hayan creado todas las copias de seguridad almacenadas con claves administradas por el servicio.  
- Cree copias de seguridad recuperables de estas claves mediante [Backup-AzureKeyVaultKey](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/backup-azurekeyvaultkey?view=azurermps-5.1.1).
- Para quitar una clave que pueda estar en peligro durante un incidente de seguridad sin arriesgarse a perder los datos, siga los pasos que se indican en [Remove a potentially compromised key](transparent-data-encryption-byok-azure-sql-remove-tde-protector.md) (Quitar una clave que pueda estar en peligro).


## <a name="high-availability-geo-replication-and-backup--restore"></a>Alta disponibilidad, replicación geográfica y copia de seguridad o restauración

### <a name="high-availability-and-disaster-recovery"></a>Alta disponibilidad y recuperación ante desastres

La forma de configurar la alta disponibilidad para Azure Key Vault depende de la configuración de la base de datos y del servidor. A continuación encontrará las configuraciones recomendadas para dos casos distintos.  En el primer caso, se trata de una base de datos o un servidor lógico independientes sin ninguna redundancia geográfica configurada.  En el segundo caso, se trata de una base de datos o servidor lógico configurados con grupos de conmutación por error o redundancia geográfica, para los cuales debe garantizarse que cada copia de redundancia geográfica tenga un almacén Azure Key Vault en el grupo de conmutación por error, a fin de que las conmutaciones por error geográficas funcionen. Para el primero, si necesita una alta disponibilidad para la base de datos y el servidor lógico sin ninguna redundancia geográfica configurada, es muy recomendable que configure el servidor para que use dos almacenes de claves distintos en dos regiones diferentes con el mismo material de clave.  Para ello, hay que crear un protector del TDE usando el almacén de claves principal colocado en la misma región que el servidor lógico y clonar la clave en un almacén de claves de otra región de Azure para que el servidor tenga acceso a un segundo almacén de claves en caso de que el principal quede interrumpido mientras la base de datos está funcionando. Use el cmdlet Backup-AzureKeyVaultKey para recuperar la clave en formato cifrado desde el almacén de claves principal y, después, use el cmdlet Restore-AzureKeyVaultKey y especifique un almacén de claves en la segunda región.


![Alta disponibilidad de servidor único y ausencia de Geo-DR](./media/transparent-data-encryption-byok-azure-sql/SingleServer_HA_Config.PNG)

## <a name="how-to-configure-geo-dr-with-azure-key-vault"></a>Cómo configurar Geo-DR con Azure Key Vault

Para conservar la alta disponibilidad de los protectores del TDE en las bases de datos cifradas, es necesario configurar almacenes de Azure Key Vault redundantes a partir de los grupos de conmutación por error de SQL Database o de las instancias de replicación geográfica activas existentes o deseados.  Cada servidor con replicación geográfica requiere un almacén de claves distinto, que debe estar colocado con el servidor en la misma región de Azure. En el caso de que una base de datos principal deje de ser accesible debido a una interrupción en una región y que se desencadene una conmutación por error, la base de datos secundaria podrá encargarse usando el almacén de claves secundario. 
 
En el caso de las bases de datos SQL de Azure con replicación geográfica, se necesita la siguiente configuración de Azure Key Vault:
- Una base de datos principal con un almacén de claves ubicado en la región y una base de datos secundaria con un almacén de claves ubicado en la región. 
- Se necesita como mínimo una base de datos secundaria (se admiten hasta cuatro bases de datos secundarias). 
- No se admiten las bases de datos secundarias de bases de datos secundarias (encadenamiento).

En la siguiente sección se tratan con más detalle los pasos de instalación y configuración. 

### <a name="azure-key-vault-configuration-steps"></a>Pasos de configuración de Azure Key Vault

- Instale [PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps?view=azurermps-5.6.0). 
- Cree dos almacenes de Azure Key Vault en dos regiones diferentes mediante [ PowerShell para habilitar la propiedad "soft-delete"](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-soft-delete-powershell) en los almacenes de claves (esta opción aún no está disponible desde el portal de Azure Key Vault, pero la requiere SQL).
- Los dos almacenes de Azure Key Vault deben estar ubicados en las dos regiones disponibles de la misma ubicación geográfica de Azure para que la copia de seguridad y la restauración de las claves funcionen.  Si necesita que los dos almacenes de claves estén en zonas geográficas diferentes para cumplir los requisitos de Geo-DR de SQL, siga el [proceso BYOK](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-hsm-protected-keys) que permite importar las claves desde un HSM local.
- Cree una clave en el primer almacén de claves:  
  - Clave RSA/RSA-HSA 2048 
  - Sin fechas de expiración 
  - La clave debe estar habilitada y debe tener permisos para llevar a cabo las operaciones get, wrap key y unwrap key 
- Haga una copia de seguridad de la clave principal y restaure la clave en el segundo almacén de claves.  Vea [BackupAzureKeyVaultKey](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/backup-azurekeyvaultkey?view=azurermps-5.1.1) y [Restore-AzureKeyVaultKey](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/restore-azurekeyvaultkey?view=azurermps-5.5.0). 

### <a name="azure-sql-database-configuration-steps"></a>Pasos de configuración de Azure SQL Database

Los siguientes pasos de configuración son diferentes en función de si se empieza con una nueva implementación de SQL o si se trabaja con una implementación de Geo-DR de SQL existente.  En primer lugar se describen los pasos de configuración de una implementación nueva y, después, se explica cómo asignar protectores del TDE almacenados en Azure Key Vault a una implementación existente que ya tiene establecido un vínculo de Geo-DR. 

Pasos para crear una implementación:
- Cree los dos servidores lógicos de SQL en las dos mismas regiones en las que se han creado antes los almacenes de claves. 
- Seleccione el panel de TDE del servidor lógico y siga estos pasos para cada servidor lógico de SQL:  
   - Seleccione el almacén de Azure Key Vault de la misma región. 
   - Seleccione la clave que se va a usar como protector del TDE: cada servidor usará la copia local del protector del TDE. 
   - Si se hace en el portal, se creará un [identificador de aplicación](https://docs.microsoft.com/en-us/azure/active-directory/managed-service-identity/overview) para el servidor lógico de SQL, que se usa para asignar los permisos lógicos de SQL Server para acceder al almacén de claves (no debe eliminar esta identidad).  El acceso se puede revocar eliminando los permisos de Azure Key Vault. para el servidor lógico de SQL, que se usa para asignar los permisos lógicos de SQL Server para acceder al almacén de claves.
- Cree la base de datos principal. 
- Siga la [guía de replicación geográfica activa](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-geo-replication-overview) para llevar a cabo el escenario. Este paso creará la base de datos secundaria.

![Grupos de conmutación por error y Geo-DR](./media/transparent-data-encryption-byok-azure-sql/Geo_DR_Config.PNG)

>[!NOTE]
>Es importante asegurarse de que estén presentes los mismos protectores del TDE en ambos almacenes de claves antes de establecer el vínculo de replicación geográfica entre las bases de datos.
>

Pasos para una base de datos de SQL existente con la implementación de Geo-DR:

Puesto que los servidores lógicos de SQL ya existen y las bases de datos principal y secundaria ya están asignadas, los pasos para configurar Azure Key Vault se deben llevar a cabo en el siguiente orden: 
- Comience con el servidor lógico de SQL que hospeda la base de datos secundaria: 
   - Asigne el almacén de claves que se encuentra en la misma región. 
   - Asigne el protector del TDE. 
- Luego, vaya al servidor lógico de SQL que hospeda la base de datos principal: 
   - Seleccione el mismo protector del TDE que se ha usado para la base de datos secundaria.
   
![Grupos de conmutación por error y Geo-DR](./media/transparent-data-encryption-byok-azure-sql/geo_DR_ex_config.PNG)

>[!NOTE]
>Al asignar el almacén de claves al servidor, es importante empezar por el servidor secundario.  En el segundo paso, asigne el almacén de claves al servidor principal y actualice el protector del TDE. El vínculo de Geo-DR seguirá funcionando porque en este momento el protector del TDE usado por la base de datos replicada está disponible para ambos servidores.
>

Antes de habilitar el TDE con claves administradas por el cliente en Azure Key Vault para un escenario de Geo-DR de SQL Database, es importante crear y mantener dos almacenes de Azure Key Vault que tengan un contenido idéntico y las mismas regiones que se usarán para la replicación geográfica de SQL Database.  "Contenido idéntico" significa que ambos almacenes de claves deben contener copias de los mismos protectores del TDE para que ambos servidores tengan acceso al uso de los protectores del TDE por parte de todas las bases de datos.  De ahora en adelante es necesario que ambos almacenes de claves estén sincronizados, lo que significa que deben contener las mismas copias de los protectores del TDE después de la rotación de claves, deben mantener las versiones anteriores de las claves usadas para los archivos de registro o las copias de seguridad, los protectores del TDE deben mantener las mismas propiedades de clave y los almacenes de claves deben mantener los mismos permisos de acceso de SQL.  
 
Siga los pasos descritos en [Introducción a la replicación geográfica activa](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview) para probar y desencadenar una conmutación por error, que debe efectuarse de forma periódica para confirmar que se han conservado los permisos de acceso de SQL a ambos almacenes de claves. 


### <a name="backup-and-restore"></a>Copias de seguridad y restauración

Desde el momento en que se cifra una base de datos con TDE mediante una clave de Key Vault, las copias de seguridad que se generan también se cifran con el mismo protector de TDE.

Para restaurar una copia de seguridad cifrada con un protector de TDE de Key Vault, asegúrese de que el material de clave aún está en el almacén original bajo el nombre de clave original. Cuando se cambia el protector de TDE para una base de datos, las copias de seguridad antiguas de la base de datos **no** se actualizan para usar el protector de TDE más reciente. Por tanto, se recomienda mantener todas las versiones antiguas del protector de TDE en Key Vault de modo que se puedan restaurar las copias de seguridad de base de datos. 

Si una clave que podría ser necesaria para restaurar una copia de seguridad ya no se encuentra en su almacén de claves original, se devuelve el siguiente mensaje de error: "Target server <Servername> does not have access to all AKV Uris created between <Timestamp #1> and <Timestamp #2>. Vuelva a intentarlo después de restaurar todos los URI de AKV."

Para mitigarlo, ejecute el cmdlet [Get-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey) para devolver la lista de claves de Key Vault que se han agregado al servidor, a menos que un usuario las haya eliminado. Para asegurarse de que se puedan restaurar todas las copias de seguridad, compruebe que el servidor de destino para la copia de seguridad tenga acceso a todas estas claves.

   ```powershell
   Get-AzureRmSqlServerKeyVaultKey `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName>
   ```
Para más información sobre la recuperación de copia de seguridad para SQL Database, vea [Recuperación de una Base de datos SQL de Azure mediante copias de seguridad automatizadas](https://docs.microsoft.com/azure/sql-database/sql-database-recovery-using-backups). Si quiere saber más sobre la recuperación de copias de seguridad para SQL Data Warehouse, vea [Restauración de SQL Data Warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-restore-database-overview).


Para la copia de seguridad de archivos de registro tenga también en cuenta que los archivos de registro que se han copiado permanecen cifrados con el sistema de cifrado de TDE original, aunque se haya cambiado de protector de TDE y la base de datos use ahora un nuevo protector de TDE.  Durante la restauración, se necesitarán las dos claves para restaurar la base de datos.  Si el archivo de registro está usando un protector de TDE almacenado en Azure Key Vault, se necesitará esta clave durante la restauración, aunque mientras tanto se haya cambiado la base de datos para usar TDE administrado del servicio.


