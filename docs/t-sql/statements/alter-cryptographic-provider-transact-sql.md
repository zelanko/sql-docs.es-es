---
title: "Modificar proveedor de servicios CRIPTOGRÁFICO (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 04/20/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_CRYPTOGRAPHIC_PROVIDER_TSQL
- ALTER CRYPTOGRAPHIC PROVIDER
- ALTER_CRYPTOGRAPHIC_TSQL
- ALTER CRYPTOGRAPHIC
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER CRYPTOGRAPHIC PROVIDER
ms.assetid: 876b6348-fb29-49e1-befc-4217979f6416
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b1579fb75de53747a26e647f69c7fc70346738fa
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="alter-cryptographic-provider-transact-sql"></a>ALTER CRYPTOGRAPHIC PROVIDER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifica un proveedor criptográfico dentro de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a partir de un proveedor de Administración extensible de claves (EKM).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
ALTER CRYPTOGRAPHIC PROVIDER provider_name   
    [ FROM FILE = path_of_DLL ]  
    ENABLE | DISABLE  
```  
  
## <a name="arguments"></a>Argumentos  
 *NombreProveedor*  
 Nombre del proveedor de Administración extensible de claves.  
  
 *Path_of_DLL*  
 Ruta de acceso del archivo .dll que implementa la interfaz de Administración extensible de claves de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ENABLE | DISABLE  
 Habilita o deshabilita un proveedor.  
  
## <a name="remarks"></a>Comentarios  
 Si el proveedor cambia el archivo .dll que se utiliza para implementar la Administración extensible de claves en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], es preciso utilizar la instrucción ALTER CRYPTOGRAPHIC PROVIDER.  
  
 Cuando la ruta de acceso del archivo .dll se actualiza mediante la instrucción ALTER CRYPTOGRAPHIC PROVIDER, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] realiza las acciones siguientes:  
-   Deshabilita el proveedor.  
-   Comprueba la firma de la DLL y se asegura de que el archivo .dll tiene el mismo GUID que el grabado en el catálogo.  
-   Actualiza la versión de DLL en el catálogo.  
  

Cuando un proveedor de EKM se establece en DISABLE, se producirá un error si en las nuevas conexiones se intenta usar el proveedor con instrucciones de cifrado.  
  
Para deshabilitar un proveedor, todas las sesiones que lo utilizan deben terminarse.  
  
Cuando una DLL del proveedor de EKM no implementa todos los métodos necesarios, ALTER CRYPTOGRAPHIC PROVIDER puede devolver el error 33085:  
  
 `One or more methods cannot be found in cryptographic provider library '%.*ls'.`  
  
Cuando el archivo de encabezado utilizado para crear la DLL del proveedor de EKM no está actualizado, ALTER CRYPTOGRAPHIC PROVIDER puede devolver el error 33032:  
  
 `SQL Crypto API version '%02d.%02d' implemented by provider is not supported. Supported version is '%02d.%02d'.`  
  
## <a name="permissions"></a>Permissions  
 Necesita el permiso CONTROL en el proveedor criptográfico.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se modifica un proveedor criptográfico, denominado `SecurityProvider` en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a una versión más reciente de un archivo .dll. Esta nueva versión se denomina `c:\SecurityProvider\SecurityProvider_v2.dll` y se instala en el servidor. El certificado del proveedor debe estar instalado en el servidor.  
  
1. Deshabilitar el proveedor para llevar a cabo la actualización. Esto finalizará todas las criptográficas sesiones abiertas.  
```  
ALTER CRYPTOGRAPHIC PROVIDER SecurityProvider   
DISABLE;  
GO  
```  

2. Actualice el archivo DLL del proveedor. El GUID debe ser el mismo que la versión anterior, pero la versión puede ser diferente.  
```  
ALTER CRYPTOGRAPHIC PROVIDER SecurityProvider  
FROM FILE = 'c:\SecurityProvider\SecurityProvider_v2.dll';  
GO  
```  

3. Habilitar al proveedor actualizado.   
```  
ALTER CRYPTOGRAPHIC PROVIDER SecurityProvider   
ENABLE;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Administración extensible de claves &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/create-cryptographic-provider-transact-sql.md)   
 [DROP CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-cryptographic-provider-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [Administración extensible de claves con el Almacén de claves de Azure &#40;SQL Server&#41;](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
  

