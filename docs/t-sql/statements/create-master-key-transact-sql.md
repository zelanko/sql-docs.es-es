---
title: CREATE MASTER KEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d885d5001c777eeb9a68732aa907c7e37be352c3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47644589"
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
 PASSWORD ='*password*'  
 Es la contraseña usada para cifrar la clave maestra de la base de datos. *password* debe cumplir los requisitos de la directiva de contraseñas de Windows del equipo que ejecuta la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *password* es opcional en [!INCLUDE[ssSDS](../../includes/sssds-md.md)] y [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)].  
  
## <a name="remarks"></a>Notas  
 La clave maestra de base de datos es una clave simétrica que se usa para proteger las claves privadas de certificados y las claves asimétricas presentes en la base de datos. Al crearla, la clave maestra se cifra mediante el algoritmo AES_256 y una contraseña proporcionada por el usuario. En [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], se utiliza el algoritmo triple DES. Para permitir el descifrado automático de la clave maestra, se cifra una copia de la clave mediante la clave maestra de servicio y se almacena en la base de datos y en la base de datos maestra. Por lo general, la copia almacenada en la base de datos maestra se actualiza automáticamente al cambiar la clave maestra. Es posible cambiar esta opción predeterminada usando la opción DROP ENCRYPTION BY SERVICE MASTER KEY de [ALTER MASTER KEY](../../t-sql/statements/alter-master-key-transact-sql.md). Para abrir una clave maestra que no se haya cifrado con la clave maestra de servicio, debe usarse la instrucción [OPEN MASTER KEY](../../t-sql/statements/open-master-key-transact-sql.md) y una contraseña.  
  
 La columna is_master_key_encrypted_by_server de la vista de catálogo sys.databases de la base de datos maestra indica si la clave maestra de la base de datos se ha cifrado con la clave maestra de servicio.  
  
 Puede ver la información acerca de la clave maestra de base de datos en la vista de catálogo sys.symmetric_keys.  

Para el Almacenamiento de datos paralelos de SQL Server, la clave maestra normalmente está protegida por la clave maestra de servicio y al menos una contraseña. En caso de que la base de datos se mueva físicamente a otro servidor (trasvase de registros, restauración de la copia de seguridad, etc.), la base de datos contendrá una copia de la clave maestra cifrada por la clave maestra de servicio del servidor original (a menos que el cifrado se haya quitado explícitamente mediante ALTER MASTER KEY DDL) y una copia de ella misma cifrada por cada contraseña especificada durante CREATE MASTER KEY o las operaciones ALTER MASTER KEY DDL posteriores. Después de haber movido la base de datos, para poder de recuperar la clave maestra y todos los datos cifrados con la clave maestra como la raíz de la jerarquía de claves, el usuario tendrá que usar la instrucción OPEN MASTER KEY con una de las contraseñas usadas para proteger la clave maestra, o bien tendrá que restaurar una copia de seguridad de la clave maestra o restaurar una copia de seguridad de la clave maestra de servicio original en el nuevo servidor. 

Para [!INCLUDE[ssSDS](../../includes/sssds-md.md)] y [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)], la protección por contraseña no se considera un mecanismo de seguridad para evitar la pérdida de datos en situaciones en las que se haya movido la base de datos de un servidor a otro, ya que la protección mediante clave maestra de servicio en la clave maestra está administrada por la plataforma Microsoft Azure. Por tanto, la contraseña de clave maestra es opcional en [!INCLUDE[ssSDS](../../includes/sssds-md.md)] y [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)].
  
> [!IMPORTANT]  
>  Debe realizar una copia de seguridad de la clave maestra mediante [BACKUP MASTER KEY](../../t-sql/statements/backup-master-key-transact-sql.md) y almacenar la copia de seguridad en un lugar seguro y fuera de las instalaciones.  
  
 La clave maestra de servicio y las claves maestras de base de datos se protegen mediante el algoritmo AES-256.  
  
## <a name="permissions"></a>Permisos  
 Necesita el permiso CONTROL en la base de datos.  
  
## <a name="examples"></a>Ejemplos  
 En este ejemplo se crea una clave maestra de base de datos para la base de datos actual. La clave se cifra con la contraseña `23987hxJ#KL95234nl0zBe`.  
  
```  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '23987hxJ#KL95234nl0zBe';  
GO  
```  

  
## <a name="see-also"></a>Ver también  
 [sys.symmetric_keys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [OPEN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/open-master-key-transact-sql.md)   
 [ALTER MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md)   
 [DROP MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-master-key-transact-sql.md)   
 [CLOSE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/close-master-key-transact-sql.md)   
 [Jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  


