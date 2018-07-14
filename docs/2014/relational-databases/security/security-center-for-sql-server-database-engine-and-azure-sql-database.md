---
title: Centro de seguridad para el motor de base de datos SQL Server y Azure SQL Database | Microsoft Docs
ms.custom: ''
ms.date: 09/23/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- Security [SQL Server]
helpviewer_keywords:
- SQL Server, security
- security [SQL Server]
- database security [SQL Server]
- databases [SQL Server], security
ms.assetid: dfb39d16-722a-4734-94bb-98e61e014ee7
caps.latest.revision: 50
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 7135846a7d442f9f43bfac505ed35a903c6b874a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37283101"
---
# <a name="security-center-for-sql-server-database-engine-and-azure-sql-database"></a>Centro de seguridad para el motor de base de datos SQL Server y la base de datos SQL Azure
  En esta página se proporcionan vínculos para ayudarle a buscar la información que necesita sobre seguridad y protección en [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]y [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)].  
  
> [!NOTE]  
>  Las capacidades de [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] siguen mejorando. Consulte la versión más reciente de este tema para obtener la información más actual de [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
|Autenticación: ¿Quién es usted?|Autorización: ¿Qué puede hacer?|Cifrado: Almacenamiento de datos secretos|Seguridad de conexión: Restringir y proteger|Auditoría: Acceso a la grabación|  
|----------------------------------|-------------------------------------|-------------------------------------|---------------------------------------------------|--------------------------------|  
|**¿Quién autentica?**<br /><br /> [![Mapa del centro de seguridad Windows autenticación](../../database-engine/media/security-center-map-windows-authenticaion.png "mapa del centro de seguridad autenticación de Windows")](http://msdn.microsoft.com/library/ms144284.aspx)<br /><br /> <br /><br /> [![Autenticación de SQL Server de centro de seguridad mapa](../../database-engine/media/security-center-map-sql-authenticaion.png "autenticación de SQL Server de mapa de centro de seguridad")](http://msdn.microsoft.com/library/ms144284.aspx)<br /><br /> **¿Dónde se autentica?**<br /><br /> [![Centro de seguridad asignar inicios de sesión y usuarios](../../database-engine/media/security-center-map-logins-users.png "centro de seguridad asignar inicios de sesión y usuarios")](http://msdn.microsoft.com/library/aa337562.aspx)<br /><br /> <br /><br /> [![Los usuarios de base de datos de contenido de mapa del centro de seguridad](../../database-engine/media/security-center-map-contained-users.png "usuarios de base de datos de contenidos de mapa del centro de seguridad")](http://msdn.microsoft.com/library/ff929188.aspx)<br /><br /> **Utilizando otras identidades**<br /><br /> [![Las credenciales de mapa del centro de seguridad](../../database-engine/media/security-center-map-credentials.png "las credenciales de mapa del centro de seguridad")](http://msdn.microsoft.com/library/ms161950.aspx)<br /><br /> [![Mapa del centro de seguridad Execute As Login](../../database-engine/media/security-center-map-exec-as-login.png "mapa del centro de seguridad Execute As Login")](http://msdn.microsoft.com/library/ms181362.aspx)<br /><br /> [![Mapa del centro de seguridad se ejecute como usuario](../../database-engine/media/security-center-map-exec-as-user.png "mapa del centro de seguridad se ejecute como usuario")](http://msdn.microsoft.com/library/ms181362.aspx)<br /><br /> ![Marcador de posición](../../database-engine/media/security-center-map-blankplaceholder.png "marcador de posición")<br /><br /> ![Marcador de posición](../../database-engine/media/security-center-map-blankplaceholder.png "marcador de posición")<br /><br /> ![Marcador de posición](../../database-engine/media/security-center-map-blankplaceholder.png "marcador de posición")<br /><br /> ![Marcador de posición](../../database-engine/media/security-center-map-blankplaceholder.png "marcador de posición")|**Conceder, revocar y denegar permisos**<br /><br /> [![Centro de seguridad se asignan las clases protegibles](../../database-engine/media/security-center-map-securable-classes.png "centro de seguridad se asignan las clases protegibles")](http://msdn.microsoft.com/library/ms190401.aspx)<br /><br /> [![Mapa del centro de seguridad permisos de servidor](../../database-engine/media/security-center-map-srv-perms.png "mapa del centro de seguridad permisos de servidor")](http://msdn.microsoft.com/library/ms191291.aspx)<br /><br /> [![Base de datos de mapa del centro de seguridad permisos](../../database-engine/media/security-center-map-db-perms.png "permisos de base de datos de mapa de centro de seguridad")](http://msdn.microsoft.com/library/ms191291.aspx)<br /><br /> **Seguridad por roles**<br /><br /> [![Mapa del centro de seguridad Roles de servidor](../../database-engine/media/security-center-map-srv-roles.png "Roles de servidor de asignación de centro de seguridad")](http://msdn.microsoft.com/library/ms188659.aspx)<br /><br /> [![Roles de base de datos de mapa de Security Center](../../database-engine/media/security-center-map-db-roles.png "Roles de base de datos de mapa de Security Center")](http://msdn.microsoft.com/library/ms189121.aspx)<br /><br /> `Restricting Data Access to Selected Data Elements`<br /><br /> [![Vistas de mapa del centro de seguridad y procedimientos](../../database-engine/media/security-center-map-view-procs.png "procedimientos y vistas de mapa del centro de seguridad")](http://msdn.microsoft.com/library/ms175503.aspx)<br /><br /> [![Seguridad de nivel de fila de la asignación de centro de seguridad](../../database-engine/media/security-center-map-row-level-sec.png "seguridad de nivel de fila de la asignación de centro de seguridad")](http://msdn.microsoft.com/library/dn765131.aspx)<br /><br /> [![Enmascaramiento dinámico de datos de mapa de centro de seguridad](../../database-engine/media/security-center-map-data-masking.png "enmascaramiento dinámico de datos de mapa de centro de seguridad")](http://azure.microsoft.com/documentation/articles/sql-database-dynamic-data-masking-get-started/)<br /><br /> [![Mapa del centro de seguridad de objetos firmados](../../database-engine/media/security-center-map-signed-objects.png "mapa del centro de seguridad de objetos firmados")](http://msdn.microsoft.com/library/ms181700.aspx)<br /><br /> ![Marcador de posición](../../database-engine/media/security-center-map-blankplaceholder.png "marcador de posición")|**Cifrado de archivos:**<br /><br /> [![BitLocker de mapa del centro de seguridad](../../database-engine/media/security-center-map-bitlocker.png "BitLocker de mapa del centro de seguridad")](http://support.microsoft.com/en-us/kb/2855131)<br /><br /> [![Mapa del centro de seguridad cifrado de NTFS](../../database-engine/media/security-center-map-ntfs-encryp.png "mapa del centro de seguridad cifrado de NTFS")](http://msdn.microsoft.com/library/dd163562.aspx)<br /><br /> [![Mapa del centro de seguridad TDE](../../database-engine/media/security-center-map-tde.png "mapa del centro de seguridad TDE")](http://msdn.microsoft.com/library/bb934049.aspx)<br /><br /> [![Mapa del centro de seguridad, copia de seguridad cifrado](../../database-engine/media/security-center-map-backup-encryp.png "mapa del centro de seguridad, copia de seguridad cifrado")](http://msdn.microsoft.com/library/dn449489.aspx)<br /><br /> **Orígenes de cifrado**<br /><br /> [![Mapa del centro de seguridad EKM](../../database-engine/media/security-center-map-ekm.png "mapa del centro de seguridad EKM")](http://msdn.microsoft.com/library/bb895340.aspx)<br /><br /> [![Mapa del centro de seguridad de Azure Key Vault](../../database-engine/media/security-center-map-key-vault.png "mapa del centro de seguridad de Azure Key Vault")](http://azure.microsoft.com/documentation/articles/key-vault-get-started/)<br /><br /> **Columnas, datos y cifrado de claves**<br /><br /> [![Mapa del centro de seguridad cifrado mediante certificado](../../database-engine/media/security-center-map-cert.png "mapa del centro de seguridad cifrado mediante certificado")](http://msdn.microsoft.com/library/ms188061.aspx)<br /><br /> [![Mapa del centro de seguridad cifrado mediante clave simétrica](../../database-engine/media/security-center-map-sym-key.png "mapa del centro de seguridad cifrado mediante clave simétrica")](http://msdn.microsoft.com/library/ms174361.aspx)<br /><br /> [![Mapa del centro de seguridad cifrado mediante clave asimétrica](../../database-engine/media/security-center-map-asym-key.png "mapa del centro de seguridad cifrado mediante clave asimétrica")](http://msdn.microsoft.com/library/ms186950.aspx)<br /><br /> [![Mapa del centro de seguridad cifrado mediante frase de contraseña](../../database-engine/media/security-center-map-passphrase.png "mapa del centro de seguridad cifrado mediante frase de contraseña")](http://msdn.microsoft.com/library/ms190357.aspx)|**Protección de Firewall**<br /><br /> [![Mapa del centro de seguridad, Windows Firewall](../../database-engine/media/security-center-map-windows-firewall.png "mapa del centro de seguridad, Windows Firewall")](http://msdn.microsoft.com/library/ms175043.aspx)<br /><br /> [![Mapa del centro de seguridad, Firewall Service](../../database-engine/media/security-center-map-service-firewall.png "mapa del centro de seguridad, Firewall Service")](http://msdn.microsoft.com/library/azure/ee621782.aspx)<br /><br /> [![Base de datos de mapa del centro de seguridad Firewall](../../database-engine/media/security-center-map-db-firewall.png "Firewall de base de datos de mapa de centro de seguridad")](http://msdn.microsoft.com/library/azure/ee621782.aspx)<br /><br /> **Cifrar los datos en tránsito**<br /><br /> [![Mapa del centro de seguridad SSL forzada](../../database-engine/media/security-center-map-forced-ssl.png "mapa del centro de seguridad SSL forzada")](http://msdn.microsoft.com/library/ms191192.aspx)<br /><br /> [![Mapa del centro de seguridad SSL opcional](../../database-engine/media/security-center-map-opt-ssl.png "mapa del centro de seguridad SSL opcional")](http://msdn.microsoft.com/library/ms191192.aspx)<br /><br /> ![Marcador de posición](../../database-engine/media/security-center-map-blankplaceholder.png "marcador de posición")<br /><br /> ![Marcador de posición](../../database-engine/media/security-center-map-blankplaceholder.png "marcador de posición")<br /><br /> ![Marcador de posición](../../database-engine/media/security-center-map-blankplaceholder.png "marcador de posición")<br /><br /> ![Marcador de posición](../../database-engine/media/security-center-map-blankplaceholder.png "marcador de posición")<br /><br /> ![Marcador de posición](../../database-engine/media/security-center-map-blankplaceholder.png "marcador de posición")<br /><br /> ![Marcador de posición](../../database-engine/media/security-center-map-blankplaceholder.png "marcador de posición")<br /><br /> ![Marcador de posición](../../database-engine/media/security-center-map-blankplaceholder.png "marcador de posición")|**Auditoría automatizada**<br /><br /> [![Centro de seguridad mapa auditoría de SQL Server](../../database-engine/media/security-center-map-sql-audit.png "centro de seguridad mapa auditoría de SQL Server")](http://msdn.microsoft.com/library/cc280386.aspx)<br /><br /> [![Auditoría de base de datos SQL de centro de seguridad mapa](../../database-engine/media/security-center-map-sqldb-audit.png "centro de seguridad mapa de auditoría de base de datos SQL")](http://azure.microsoft.com/documentation/articles/sql-database-auditing-get-started/)<br /><br /> **Auditoría personalizada**<br /><br /> ![Marcador de posición](../../database-engine/media/security-center-map-blankplaceholder.png "marcador de posición")<br /><br /> [![Los desencadenadores de mapa del centro de seguridad](../../database-engine/media/security-center-map-triggers.png "desencadenadores de mapa del centro de seguridad")](http://msdn.microsoft.com/library/ms175941.aspx)<br /><br /> **Cumplimiento**<br /><br /> [![SecCtrCompliance](../../database-engine/media/secctrcompliance.png "SecCtrCompliance")](http://azure.microsoft.com/support/trust-center/services/)<br /><br /> ![Marcador de posición](../../database-engine/media/security-center-map-blankplaceholder.png "marcador de posición")<br /><br /> ![Marcador de posición](../../database-engine/media/security-center-map-blankplaceholder.png "marcador de posición")<br /><br /> ![Marcador de posición](../../database-engine/media/security-center-map-blankplaceholder.png "marcador de posición")<br /><br /> ![Marcador de posición](../../database-engine/media/security-center-map-blankplaceholder.png "marcador de posición")<br /><br /> ![Marcador de posición](../../database-engine/media/security-center-map-blankplaceholder.png "marcador de posición")<br /><br /> ![Leyenda del centro de seguridad](../../database-engine/media/security-center-map-legend.png "leyenda del centro de seguridad")|  
  
## <a name="links-to-specific-related-topics"></a>Vínculos a temas relacionados específicos  
 ![Icono pequeño de carpeta de archivo](../../integration-services/media/filefolder-small.gif "icono pequeño de carpeta de archivo") **autenticación: ¿quién es usted?**  
 **¿Quién autentica? (Windows o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])**  
  
-   [Elegir un modo de autenticación](choose-an-authentication-mode.md)  
  
 **Autenticación en la base de datos maestra** (inicios de sesión y usuarios de base de datos)  
  
-   [Crear un inicio de sesión de SQL Server](authentication-access/create-a-login.md)  
  
-   [Administración de bases de datos e inicios de sesión de la base de datos SQL Azure](http://msdn.microsoft.com/library/ee336235.aspx)  
  
-   [Crear un usuario de base de datos](authentication-access/create-a-database-user.md)  
  
 **Autenticación en una base de datos de usuario**  
  
-   [Usuarios de base de datos independiente: hacer que la base de datos sea portátil](contained-database-users-making-your-database-portable.md)  
  
 **Utilizando otras identidades**  
  
-   [Credenciales &#40;motor de base de datos&#41;](authentication-access/credentials-database-engine.md)  
  
-   [Ejecutar como otro inicio de sesión](/sql/t-sql/statements/execute-as-transact-sql)  
  
-   [Ejecutar como otro usuario de base de datos](/sql/t-sql/statements/execute-as-transact-sql)  
  
 ![Icono carpeta de archivos pequeños](../../integration-services/media/filefolder-small.gif "archivo pequeño icono de carpeta") **cifrado: almacenamiento de datos secretos**  
 **Cifrado de archivos:**  
  
-   [BitLocker (nivel de unidad)](http://support.microsoft.com/kb/2855131)  
  
-   [Cifrado de NTFS (nivel de carpeta)](http://msdn.microsoft.com/library/dd163562.aspx)  
  
-   [Cifrado de datos transparente (nivel de archivo)](encryption/transparent-data-encryption.md)  
  
-   [Cifrado de copia de seguridad (nivel de archivo)](../backup-restore/backup-encryption.md)  
  
 **Orígenes de cifrado**  
  
-   [Módulo de administración extensible de claves](encryption/extensible-key-management-ekm.md)  
  
-   [Claves almacenadas en el Almacén de claves de Azure](encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
 **Columna, datos y cifrado de claves**  
  
-   [Cifrar mediante certificados](/sql/t-sql/functions/encryptbycert-transact-sql)  
  
-   [Cifrar mediante clave asimétrica](/sql/t-sql/functions/encryptbyasymkey-transact-sql)  
  
-   [Cifrar mediante clave simétrica](/sql/t-sql/functions/encryptbykey-transact-sql)  
  
-   [Cifre mediante frase de contraseña](/sql/t-sql/functions/encryptbypassphrase-transact-sql)  
  
 ![Icono pequeño de carpeta de archivo](../../integration-services/media/filefolder-small.gif "icono pequeño de carpeta de archivo") **autorización: ¿para qué sirven?**  
 **Conceder, revocar y denegar permisos**  
  
-   [Jerarquía de permisos &#40;motor de base de datos&#41;](permissions-hierarchy-database-engine.md)  
  
-   [Permisos](permissions-database-engine.md)  
  
-   [Elementos protegibles](securables.md)  
  
 **Seguridad por roles**  
  
-   [Roles de nivel de servidor](authentication-access/server-level-roles.md)  
  
-   [Roles de nivel de base de datos](authentication-access/database-level-roles.md)  
  
 `Restricting Data Access to Selected Data Elements`  
  
-   Restricción del acceso a datos mediante [Vistas](../views/views.md) y [Procedimientos](../stored-procedures/stored-procedures-database-engine.md)  
  
-   [Seguridad de nivel de fila](http://msdn.microsoft.com/library/azure/dn765131.aspx)  
  
-   [Enmascaramiento de datos dinámicos](http://azure.microsoft.com/documentation/articles/sql-database-dynamic-data-masking-get-started/)  
  
-   [Objetos firmados](/sql/t-sql/statements/add-signature-transact-sql)  
  
 ![Icono carpeta de archivos pequeños](../../integration-services/media/filefolder-small.gif "archivo pequeño icono de carpeta") **seguridad de conexión: restringir y proteger**  
 **Protección de Firewall**  
  
-   [Configurar Firewall de Windows para el acceso al motor de base de datos](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)  
  
-   [Configuración de firewall de la base de datos SQL Azure](/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database)  
  
-   [Configuración de Firewall del servicio Azure](/sql/relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database)  
  
 **Cifrar los datos en tránsito**  
  
-   [Capa de sockets seguros para el motor de base de datos](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)  
  
-   [Capa de sockets seguros para la base de datos SQL](https://msdn.microsoft.com/library/azure/ff394108.aspx)  
  
 ![Icono carpeta de archivos pequeños](../../integration-services/media/filefolder-small.gif "archivo pequeño icono de carpeta") **auditoría: acceso a la grabación**  
 **Auditoría automatizada**  
  
-   [SQL Server Audit &#40;motor de base de datos&#41;](auditing/sql-server-audit-database-engine.md)  
  
-   [Auditoría de base de datos SQL](http://azure.microsoft.com/documentation/articles/sql-database-auditing-get-started/)  
  
 **Implementación de auditoría personalizada**  
  
-   Crear [DDL Triggers](../triggers/ddl-triggers.md) y [DML Triggers](../triggers/dml-triggers.md)  
  
 ![Icono carpeta de archivos pequeños](../../integration-services/media/filefolder-small.gif "archivo pequeño icono de carpeta") **cumplimiento**  
 **SQL Server**  
  
-   [criterios comunes](http://go.microsoft.com/fwlink/?LinkId=616319)  
  
 **SQL Database**  
  
-   [Centro de confianza de Microsoft Azure: cumplimiento por característica](http://azure.microsoft.com/support/trust-center/services/)  
  
## <a name="see-also"></a>Vea también  
 [Proteger SQL Server](securing-sql-server.md)   
 [Entidades de seguridad &#40;motor de base de datos&#41;](authentication-access/principals-database-engine.md)   
 [Certificados y claves asimétricas de SQL Server](sql-server-certificates-and-asymmetric-keys.md)   
 [Cifrado de SQL Server](encryption/sql-server-encryption.md)   
 [Configuración de Área expuesta](surface-area-configuration.md)   
 [Contraseñas seguras](strong-passwords.md)   
 [Propiedad de base de datos TRUSTWORTHY](trustworthy-database-property.md)   
 [Características y tareas del motor de base de datos](../../database-engine/database-engine-features-and-tasks.md)  
  
  
