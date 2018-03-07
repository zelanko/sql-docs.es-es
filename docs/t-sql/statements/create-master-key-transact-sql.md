---
title: CREAR la clave maestra (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 04/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE_MASTER_KEY_TSQL
- MASTER_KEY_TSQL
- MASTER KEY
- CREATE MASTER KEY
dev_langs:
- TSQL
helpviewer_keywords:
- encryption [SQL Server], Database Master Key
- database master key [SQL Server]
- CREATE MASTER KEY statement
- cryptography [SQL Server], Database Master Key
- database master key [SQL Server], creating
ms.assetid: 1710a305-1a4f-48ec-836c-11ffd0356d76
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: aaec4d28dc95d792faa6406ef68df50167d0f091
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="create-master-key-transact-sql"></a>CREATE MASTER KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Crea una clave maestra de base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server and Parallel Data Warehouse  
  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password'  
[ ; ]  
```  
  
```  
-- Syntax for Azure SQL Database and Azure SQL Data Warehouse  
  
CREATE MASTER KEY [ ENCRYPTION BY PASSWORD ='password' ]
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 CONTRASEÑA ='*contraseña*'  
 Es la contraseña usada para cifrar la clave maestra de la base de datos. *contraseña* debe cumplir los requisitos de directiva de contraseñas de Windows del equipo que ejecuta la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *contraseña* es opcional en [!INCLUDE[ssSDS](../../includes/sssds-md.md)] y [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)].  
  
## <a name="remarks"></a>Comentarios  
 La clave maestra de base de datos es una clave simétrica que se usa para proteger las claves privadas de certificados y las claves asimétricas presentes en la base de datos. Al crearla, la clave maestra se cifra mediante el algoritmo AES_256 y una contraseña proporcionada por el usuario. En [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], se utiliza el algoritmo triple DES. Para permitir el descifrado automático de la clave maestra, se cifra una copia de la clave mediante la clave maestra de servicio y se almacena en la base de datos y en la base de datos maestra. Por lo general, la copia almacenada en la base de datos maestra se actualiza automáticamente al cambiar la clave maestra. Este comportamiento predeterminado se puede cambiar mediante la opción DROP ENCRYPTION BY SERVICE MASTER KEY de [ALTER MASTER KEY](../../t-sql/statements/alter-master-key-transact-sql.md). Una clave maestra que no está cifrada con la clave maestra de servicio debe abrirse mediante el uso de la [OPEN MASTER KEY](../../t-sql/statements/open-master-key-transact-sql.md) instrucción y una contraseña.  
  
 La columna is_master_key_encrypted_by_server de la vista de catálogo sys.databases de la base de datos maestra indica si la clave maestra de la base de datos se ha cifrado con la clave maestra de servicio.  
  
 Puede ver la información acerca de la clave maestra de base de datos en la vista de catálogo sys.symmetric_keys.  

Para SQL Server y almacenamiento de datos paralelos, la clave maestra normalmente está protegido mediante la clave maestra de servicio y al menos una contraseña. En el caso de la base de datos que se mueven físicamente en un servidor diferente (trasvase de registros, restaurar la copia de seguridad, etc.), la base de datos contendrá una copia de la clave maestra cifrada por la clave maestra de servicio de servidor original (a menos que el cifrado se ha quitado explícitamente mediante ALTER MASTER KEY DDL) y una copia del mismo cifrados por cada contraseña especificada durante CREATE MASTER KEY o las operaciones ALTER MASTER KEY DDL posteriores. Con el fin de recuperar la clave maestra y todos los datos cifrados con la clave maestra como la raíz de la jerarquía de claves después de que se ha movido la base de datos, el usuario tendrá usar instrucción OPEN MASTER KEY mediante uno de la contraseña utilizada para proteger la clave maestra , restaurar una copia de seguridad de la clave maestra, o restaurar una copia de seguridad de la clave maestra de servicio original en el nuevo servidor. 

Para [!INCLUDE[ssSDS](../../includes/sssds-md.md)] y [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)], la protección por contraseña no se considera como un mecanismo de seguridad para evitar que un escenario de pérdida de datos en situaciones donde se puede mover la base de datos de un servidor a otro, tal y como la protección de clave maestra de servicio en la clave maestra es administrado por la plataforma Microsoft Azure. Por lo tanto, es opcional en la contraseña de la clave maestra de la [!INCLUDE[ssSDS](../../includes/sssds-md.md)] y [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)].
  
> [!IMPORTANT]  
>  Debe hacer copia de seguridad de la clave maestra mediante [clave maestra de la copia de seguridad](../../t-sql/statements/backup-master-key-transact-sql.md) y almacenar la copia de seguridad en una ubicación segura fuera del sitio.  
  
 La clave maestra de servicio y las claves maestras de base de datos se protegen mediante el algoritmo AES-256.  
  
## <a name="permissions"></a>Permissions  
 Necesita el permiso CONTROL en la base de datos.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea una clave maestra de base de datos para la base de datos actual. La clave se cifra con la contraseña `23987hxJ#KL95234nl0zBe`.  
  
```  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '23987hxJ#KL95234nl0zBe';  
GO  
```  

  
## <a name="see-also"></a>Vea también  
 [Sys.symmetric_keys &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [Abra la clave maestra &#40; Transact-SQL &#41;](../../t-sql/statements/open-master-key-transact-sql.md)   
 [ALTER MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md)   
 [DROP MASTER KEY &#40; Transact-SQL &#41;](../../t-sql/statements/drop-master-key-transact-sql.md)   
 [CLOSE MASTER KEY &#40; Transact-SQL &#41;](../../t-sql/statements/close-master-key-transact-sql.md)   
 [Jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  


