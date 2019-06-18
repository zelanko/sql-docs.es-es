---
title: CREATE CRYPTOGRAPHIC PROVIDER (Transact-SQL) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE_CRYPTOGRAPHIC_TSQL
- CRYPTOGRAPHIC PROVIDER
- PROVIDER_TSQL
- CREATE CRYPTOGRAPHIC
- CREATE CRYPTOGRAPHIC PROVIDER
- CRYPTOGRAPHIC_PROVIDER_TSQL
- CREATE_CRYPTOGRAPHIC_PROVIDER_TSQL
- PROVIDER
dev_langs:
- TSQL
helpviewer_keywords:
- 33085 (Database Engine error)
- CREATE CRYPTOGRAPHIC PROVIDER statement
- 33032 (Database Engine error)
ms.assetid: 059a39a6-9d32-4d3f-965b-0a1ce75229c7
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 8ec316925fcd21a80561750665386a72f096060d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62993785"
---
# <a name="create-cryptographic-provider-transact-sql"></a>CREATE CRYPTOGRAPHIC PROVIDER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea un proveedor criptográfico dentro de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a partir de un proveedor de Administración extensible de claves (EKM).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CREATE CRYPTOGRAPHIC PROVIDER provider_name   
    FROM FILE = path_of_DLL  
```  
  
## <a name="arguments"></a>Argumentos  
 *provider_name*  
 Es el nombre del proveedor de Administración extensible de claves.  
  
 *path_of_DLL*  
 Es la ruta de acceso del archivo .dll que implementa la interfaz de Administración extensible de claves de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cuando se usa el **Conector de SQL Server para Microsoft Azure Key Vault**, la ubicación predeterminada es **'C:\Archivos de programa\Microsoft SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll'** .  
  
## <a name="remarks"></a>Notas  
 Todas las claves creadas por un proveedor harán referencia al proveedor por su GUID. El GUID se retiene para todas las versiones de la DLL.  
  
 La DLL que implementa la interfaz SQLEKM debe estar firmada digitalmente con cualquier certificado. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] comprobará la firma. Esto incluye su cadena de certificados, que debe tener su raíz instalada en la ubicación **Entidades de certificación raíz de confianza** en un sistema Windows. Si se verifica que la firma no es correcta, se producirá un error en la instrucción CREATE CRYPTOGRAPHIC PROVIDER. Para más información sobre certificados y cadenas de certificados, vea [Certificados y claves asimétricas de SQL Server](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md).  
  
 Cuando una DLL del proveedor de EKM no implementa todos los métodos necesarios, CREATE CRYPTOGRAPHIC PROVIDER puede devolver el error 33085:  
  
 `One or more methods cannot be found in cryptographic provider library '%.*ls'.`  
  
 Cuando el archivo de encabezado utilizado para crear la DLL del proveedor de EKM está anticuado, CREATE CRYPTOGRAPHIC PROVIDER puede devolver el error 33032:  
  
 `SQL Crypto API version '%02d.%02d' implemented by provider is not supported. Supported version is '%02d.%02d'.`  
  
## <a name="permissions"></a>Permisos  
 Debe disponer del permiso CONTROL SERVER o pertenecer al rol fijo de servidor **sysadmin**.  
  
## <a name="examples"></a>Ejemplos  
 En este ejemplo se crea un proveedor criptográfico llamado `SecurityProvider` en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a partir de un archivo .dll. El archivo .dll se denomina `c:\SecurityProvider\SecurityProvider_v1.dll` y se instala en el servidor. El certificado del proveedor se debe instalar primero en el servidor.  
  
```  
-- Install the provider  
CREATE CRYPTOGRAPHIC PROVIDER SecurityProvider  
    FROM FILE = 'C:\SecurityProvider\SecurityProvider_v1.dll';  
```  
  
## <a name="see-also"></a>Consulte también  
 [Administración extensible de claves &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [ALTER CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-cryptographic-provider-transact-sql.md)   
 [DROP CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-cryptographic-provider-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [Administración extensible de claves con el Almacén de claves de Azure &#40;SQL Server&#41;](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
  
