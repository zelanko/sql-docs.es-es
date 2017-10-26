---
title: CLR strict security | Microsoft Docs
description: "Cómo configurar CLR strict security en SQL Server"
ms.custom: 
ms.date: 06/20/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- clr strict security
- clr_strict_security_TSQL
- clr strict security
- strict_security_TSQL
helpviewer_keywords:
- assemblies [CLR integration], strick security
- clr strict security option
ms.assetid: 
caps.latest.revision: 0
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 54f976fac931d9cdc731f4b3e91c433d66310194
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="clr-strict-security"></a>CLR strict security   
[!INCLUDE[tsql-appliesto-ssvnxt-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]   

Controla la interpretación del permiso `SAFE`, `EXTERNAL ACCESS`, `UNSAFE` en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].   

|Valor |Descripción | 
|----- |----- | 
|0 |Deshabilitada: se proporciona para la compatibilidad con versiones anteriores. El valor `Disabled` no es recomendable. | 
|1 |Habilitada: hace que el [!INCLUDE[ssde-md](../../includes/ssde-md.md)] pase por alto la información de `PERMISSION_SET` relativa a los ensamblados y los interprete siempre como `UNSAFE`.  `Enabled` es el valor predeterminado en [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)]. | 

>  [!WARNING]
>  CLR usa la seguridad de acceso del código (CAS) de .NET Framework, que ya no se admite como un límite de seguridad. Un ensamblado CLR creado con la opción `PERMISSION_SET = SAFE` puede tener acceso a los recursos externos del sistema, llamar a código no administrado y adquirir privilegios sysadmin. A partir de [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)], se incluye una opción de `sp_configure` denominada `clr strict security` para mejorar la seguridad de los ensamblados CLR. La opción `clr strict security` está habilitada de forma predeterminada y trata los ensamblados CLR `SAFE` y `EXTERNAL_ACCESS` como si estuvieran marcados con `UNSAFE`. La opción `clr strict security` se puede deshabilitar para permitir la compatibilidad con versiones anteriores, pero no se recomienda hacerlo. Microsoft recomienda que todos los ensamblados estén firmados con un certificado o clave asimétrica con el correspondiente inicio de sesión que tenga concedido el permiso `UNSAFE ASSEMBLY` en la base de datos maestra. Los administradores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] también pueden agregar ensamblados a una lista de los ensamblados en los que el motor de base de datos debe confiar. Para más información, vea [sys.sp_add_trusted_assembly](../../relational-databases/system-stored-procedures/sys-sp-add-trusted-assembly-transact-sql.md).

## <a name="remarks"></a>Comentarios   

Cuando se habilita, la opción `PERMISSION_SET` en las instrucciones `CREATE ASSEMBLY` y `ALTER ASSEMBLY` se omite en tiempo de ejecución, pero las opciones `PERMISSION_SET` se conservan en los metadatos. Si la opción se omite, se reduce el riesgo de romper las instrucciones de código existentes.

`CLR strict security` es una `advanced option`.  

>  [!IMPORTANT]  
>  Después de habilitar la seguridad estricta, los ensamblados que no estén firmados no podrán cargarse. Debe modificar (o eliminar y volver a crear) cada ensamblado para que se firme con un certificado o clave asimétrica que tenga el inicio de sesión correspondiente con el permiso `UNSAFE ASSEMBLY` en el servidor.

## <a name="permissions"></a>Permissions 

### <a name="to-change-this-option"></a>Para cambiar esta opción  
Debe disponer del permiso `CONTROL SERVER` o pertenecer al rol fijo de servidor `sysadmin`.

### <a name="to-create-an-clr-assembly"></a>Para crear un ensamblado CLR   
Los siguientes permisos son necesarios para crear un ensamblado CLR cuando la opción `CLR strict security` está habilitada:

- El usuario debe tener el permiso `CREATE ASSEMBLY`.  
- Además, se debe dar una de las siguientes condiciones:  
  - El ensamblado debe estar firmado con un certificado o clave asimétrica que tenga el inicio de sesión correspondiente con el permiso `UNSAFE ASSEMBLY` en el servidor. Se recomienda firmar el ensamblado.  
  - La base de datos tiene la propiedad `TRUSTWORTHY` establecida en `ON` y pertenece a un inicio de sesión que tiene el permiso `UNSAFE ASSEMBLY` en el servidor. Esta opción no se recomienda.  

  
## <a name="see-also"></a>Vea también  
  
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [clr enabled (opción de configuración del servidor)](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)

