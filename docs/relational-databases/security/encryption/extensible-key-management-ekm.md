---
title: Administración extensible de claves (EKM) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Key Management
- Extensible Key Management
- EKM, described
ms.assetid: 9bfaf500-2d1e-4c02-b041-b8761a9e695b
author: aliceku
ms.author: aliceku
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: df1fe03ce3d0bf0397222ab3ef0834fac1cf6e33
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52545337"
---
# <a name="extensible-key-management-ekm"></a>Administración extensible de claves (EKM)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proporciona las funciones del cifrado de datos junto con la *Administración extensible de claves* (EKM), las cuales usan la *API criptográfica de Microsoft* (MSCAPI) para el cifrado y generación de clave. Las claves de cifrado utilizadas para cifrar datos y claves se crean en contenedores transitorios de claves y se deben exportar desde un proveedor antes de que se almacenen en la base de datos. Este enfoque permite a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]llevar a cabo la administración de claves, que incluye una jerarquía de claves de cifrado y la copia de seguridad de las claves.  
  
 Con la creciente demanda para cumplir con las leyes y con las políticas de privacidad de datos, las organizaciones están aprovechándose del cifrado como una forma de obtener una solución de "defensa en profundidad". Este enfoque es a menudo poco práctico si solo se utilizan las herramientas de administración del cifrado de base de datos. Los fabricantes de hardware proporcionan productos específicamente diseñados para la administración de claves de la empresa usando *Módulos de seguridad por hardware* (HSM). Los dispositivos HSM almacenan las claves de cifrado en módulos de hardware o de software. Ésta es una solución más segura porque las claves de cifrado no residen junto a los datos de cifrado.  
  
 Varios fabricantes proporcionan HSM tanto para administración de claves como para la aceleración del cifrado. Los dispositivos HSM utilizan interfaces hardware junto con un proceso de servidor que actúan como un intermediario entre la aplicación y HSM. Los fabricantes también implementan proveedores de MSCAPI sobre sus módulos, que pueden ser de tipo hardware o software. A menudo, MSCAPI proporciona solo un subconjunto de la funcionalidad que ofrece HSM. Los fabricantes también pueden proporcionar el software de administración para HSM, configuración de claves y acceso a claves.  
  
 Las implementaciones de HSM varían de un fabricante a otro y para poder utilizarlas con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] es necesaria una interfaz común. Aunque MSCAPI proporciona esta interfaz, admite solo un subconjunto de las características de HSM. También tiene otras limitaciones, como la incapacidad para conservar de forma nativa las claves simétricas o la falta de compatibilidad orientada a sesiones.  
  
 La Administración extensible de claves de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] permite a los fabricantes de EKM/HSM registrar sus módulos en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Cuando se registra, los usuarios de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pueden utilizar las claves de cifrado almacenadas en los módulos EKM. Esto permite a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] obtener acceso a las características de cifrado avanzadas que admiten estos módulos, como el cifrado y descifrado masivo, o las funciones de administración de claves, como el vencimiento o la rotación de claves.  
  
 Al ejecutar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en una máquina virtual de Azure, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pueden usar claves almacenadas en el [almacén de claves de Azure](https://go.microsoft.com/fwlink/?LinkId=521401). Para obtener más información, vea [Administración extensible de claves con el Almacén de claves de Azure &#40;SQL Server&#41;](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)llevar a cabo la administración de claves, que incluye una jerarquía de claves de cifrado y la copia de seguridad de las claves.  
  
## <a name="ekm-configuration"></a>Configuración de EKM  
 La Administración extensible de claves no está disponible en todas las ediciones de [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], vea [Características compatibles con las ediciones de SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 De forma predeterminada, la Administración extensible de claves está desactivada. Para habilitar esta característica, utilice el comando sp_configure, que tiene la siguiente opción y valor, tal y como se muestra en el ejemplo siguiente:  
  
```  
sp_configure 'show advanced', 1  
GO  
RECONFIGURE  
GO  
sp_configure 'EKM provider enabled', 1  
GO  
RECONFIGURE  
GO  
```  
  
> [!NOTE]  
>  Si usa el comando sp_configure para esta opción en ediciones de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que no admiten EKM, recibirá un error.  
  
 Para deshabilitar la característica, establezca el valor en **0**. Para obtener más información sobre cómo establecer las opciones de servidor, vea [sp_configure &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
## <a name="how-to-use-ekm"></a>Cómo utilizar EKM  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] La Administración extensible de claves habilita las claves de cifrado que protegen los archivos de base de datos que se almacenan en un dispositivo externo, como puede ser una tarjeta inteligente, un dispositivo USB o un módulo EKM/HSM. Esto también habilita la protección de datos para los administradores de bases de datos (exceptuando a los miembros del grupo de sysadmin). Los datos se pueden cifrar utilizando claves de cifrado a las que solo tiene acceso el usuario de la base de datos en el módulo EKM/HSM externo.  
  
 La Administración extensible de claves también ofrece las siguientes ventajas:  
  
-   Comprobación de la autorización adicional (permitiendo la separación de tareas).  
  
-   Mayor rendimiento en el cifrado o descifrado basado en hardware.  
  
-   Generación de claves de cifrado externas.  
  
-   Almacenamiento externo de la clave de cifrado (separación física de datos y claves).  
  
-   Recuperación de claves de cifrado.  
  
-   Retención de claves de cifrado externas (permite la rotación de claves de cifrado).  
  
-   Recuperación de claves de cifrado más sencilla.  
  
-   Distribución de claves de cifrado más flexible.  
  
-   Disposición de claves de cifrado segura.  
  
 Puede utilizar Administración extensible de claves con una combinación de nombre de usuario y contraseña u otros métodos definidos por el controlador EKM.  
  
> [!CAUTION]  
>  Para solucionar problemas, es posible que el soporte técnico de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] le solicite la clave de cifrado del proveedor de EKM. También podría necesitar tener acceso a las herramientas o procesos del fabricante para resolver el problema.  
  
### <a name="authentication-with-an-ekm-device"></a>Autenticación con un dispositivo EKM  
 Un módulo EKM puede admitir más de un tipo de autenticación. Cada proveedor propone únicamente un tipo de autenticación en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], es decir, si el módulo admite los tipos de autenticación básica u otros, propondrá uno u otro, pero no ambos.  
  
#### <a name="ekm-device-specific-basic-authentication-using-usernamepassword"></a>Autenticación básica específica del dispositivo EKM utilizando el nombre de usuario y contraseña  
 Para aquellos módulos EKM que admitan la autenticación básica usando una combinación de *nombre de usuario/contraseña*, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proporciona una autenticación transparente por medio de credenciales. Para obtener más información sobre las credenciales, vea [Credenciales &#40;motor de base de datos&#41;](../../../relational-databases/security/authentication-access/credentials-database-engine.md).  
  
 Se puede crear una credencial para un proveedor de EKM y asignarse a un inicio de sesión (tanto para cuentas Windows como para cuentas de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]) con el fin de obtener acceso a un módulo EKM en base a un inicio de sesión. El campo *Identify* de la credencial contiene el nombre de usuario; el campo *secret* contiene una contraseña para conectar con un módulo EKM.  
  
 Si no hay ninguna credencial de inicio de sesión asignada para el proveedor de EKM, se utiliza la credencial asignada a la cuenta de servicio de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 Un inicio de sesión puede tener varias credenciales asignadas a él, siempre y cuando se utilicen para proveedores de EKM distintos. Solo debe haber una credencial asignada por cada EKM y por cada inicio de sesión. La misma credencial puede estar asignada a otros inicios de sesión.  
  
#### <a name="other-types-of-ekm-device-specific-authentication"></a>Otros tipos de autenticación específicas del dispositivo EKM  
 Para aquellos módulos EKM que usan una autenticación que no sea la Windows o la de una combinación de *nombre de usuario/contraseña* , la autenticación se debe realizar independientemente de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
### <a name="encryption-and-decryption-by-an-ekm-device"></a>Cifrado y descifrado por parte de un dispositivo EKM  
 Puede utilizar las siguientes funciones y características para cifrar y descifrar datos utilizando claves simétricas y asimétricas:  
  
|Función o característica|Referencia|  
|-------------------------|---------------|  
|Cifrado de claves simétricas|[CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-symmetric-key-transact-sql.md)|  
|Cifrado de claves asimétricas|[CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-asymmetric-key-transact-sql.md)|  
|EncryptByKey(key_guid, "texto_no_cifrado", ...)|[ENCRYPTBYKEY &#40;Transact-SQL&#41;](../../../t-sql/functions/encryptbykey-transact-sql.md)|  
|DecryptByKey(texto_cifrado, ...)|[DECRYPTBYKEY &#40;Transact-SQL&#41;](../../../t-sql/functions/decryptbykey-transact-sql.md)|  
|EncryptByAsmKey (key_guid, 'texto no cifrado')|[ENCRYPTBYASYMKEY &#40;Transact-SQL&#41;](../../../t-sql/functions/encryptbyasymkey-transact-sql.md)|  
|DecryptByAsmKey(texto cifrado)|[DECRYPTBYASYMKEY &#40;Transact-SQL&#41;](../../../t-sql/functions/decryptbyasymkey-transact-sql.md)|  
  
#### <a name="database-keys-encryption-by-ekm-keys"></a>Cifrado de claves de la base de datos mediante claves EKM  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pueden utilizar claves EKM para cifrar otras claves de una base de datos. Puede crear y utilizar tanto claves simétricas como asimétricas en un dispositivo EKM. Puede cifrar claves simétricas nativas (no EKM) con claves asimétricas EKM.  
  
 El ejemplo siguiente crea una clave simétrica de la base de datos y la cifra utilizando una clave de un módulo EKM.  
  
```  
CREATE SYMMETRIC KEY Key1  
WITH ALGORITHM = AES_256  
ENCRYPTION BY EKM_AKey1;  
GO  
--Open database key  
OPEN SYMMETRIC KEY Key1  
DECRYPTION BY EKM_AKey1  
```  
  
 Para obtener más información sobre las claves de servidor y de base de datos en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], vea [SQL Server y claves de cifrado de base de datos &#40;motor de base de datos&#41;](../../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md).  
  
> [!NOTE]  
>  No puede cifrar una clave EKM con otra clave EKM.  
>   
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no admite la firma de módulos con las claves asimétricas generadas en el proveedor EKM.  
  
## <a name="related-tasks"></a>Related Tasks  
 [EKM provider enabled (opción de configuración del servidor)](../../../database-engine/configure-windows/ekm-provider-enabled-server-configuration-option.md)  
  
 [Habilitar TDE en SQL Server con EKM](../../../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)  
  
 [Administración extensible de claves con el Almacén de claves de Azure &#40;SQL Server&#41;](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
## <a name="see-also"></a>Ver también  
 [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../../t-sql/statements/create-cryptographic-provider-transact-sql.md)   
 [DROP CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-cryptographic-provider-transact-sql.md)   
 [ALTER CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-cryptographic-provider-transact-sql.md)   
 [sys.cryptographic_providers &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-cryptographic-providers-transact-sql.md)   
 [sys.dm_cryptographic_provider_sessions &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-cryptographic-provider-sessions-transact-sql.md)   
 [sys.dm_cryptographic_provider_properties &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-cryptographic-provider-properties-transact-sql.md)   
 [sys.dm_cryptographic_provider_algorithms &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-cryptographic-provider-algorithms-transact-sql.md)   
 [sys.dm_cryptographic_provider_keys &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-cryptographic-provider-keys-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-login-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [ALTER ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-asymmetric-key-transact-sql.md)   
 [DROP ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-asymmetric-key-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [ALTER SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-symmetric-key-transact-sql.md)   
 [DROP SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-symmetric-key-transact-sql.md)   
 [OPEN SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/open-symmetric-key-transact-sql.md)   
 [Hacer copia de seguridad y restaurar claves de cifrado de Reporting Services](../../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)   
 [Eliminar y volver a crear claves de cifrado &#40;Administrador de configuración de SSRS&#41;](../../../reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)   
 [Agregar y quitar claves de cifrado para implementaciones escaladas &#40;Administrador de configuración de SSRS&#41;](../../../reporting-services/install-windows/add-and-remove-encryption-keys-for-scale-out-deployment.md)   
 [Hacer una copia de seguridad de la clave maestra de servicio](../../../relational-databases/security/encryption/back-up-the-service-master-key.md)   
 [Restaurar la clave maestra de servicio](../../../relational-databases/security/encryption/restore-the-service-master-key.md)   
 [Crear la clave maestra de una base de datos](../../../relational-databases/security/encryption/create-a-database-master-key.md)   
 [Hacer copias de seguridad de una clave maestra de una base de datos](../../../relational-databases/security/encryption/back-up-a-database-master-key.md)   
 [Restaurar una clave maestra de base de datos](../../../relational-databases/security/encryption/restore-a-database-master-key.md)   
 [Crear claves simétricas idénticas en dos servidores](../../../relational-databases/security/encryption/create-identical-symmetric-keys-on-two-servers.md)  
  
  
