---
title: Sys.sp_add_trusted_assembly (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_add_trusted_assembly_TSQL
- sp_add_trusted_assembly
- sys.sp_add_trusted_assembly_TSQL
- sys.sp_add_trusted_assembly
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_add_trusted_assembly
ms.assetid: ''
caps.latest.revision: ''
author: tmullaney
ms.author: thmullan
manager: craigg
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 1a3791d82f0970ec6ed3e04ede69492abbcddb59
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38055780"
---
# <a name="sysspaddtrustedassembly-transact-sql"></a>Sys.sp_add_trusted_assembly (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Agrega un ensamblado a la lista de ensamblados de confianza para el servidor.

 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  


## <a name="syntax"></a>Sintaxis
```  
sp_add_trusted_assembly 
    [ @hash = ] 'value'
    [ , [ @description = ] 'description' ]
```  

## <a name="remarks"></a>Notas  

Este procedimiento agrega un ensamblado a [sys.trusted_assemblies](../../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md).

## <a name="arguments"></a>Argumentos

[ @hash =] '*valor*'  
El valor de hash SHA2_512 del ensamblado que se va a agregar a la lista de ensamblados de confianza para el servidor. Puede que se cargue cuando los ensamblados de confianza [seguridad estricta de CLR](../../database-engine/configure-windows/clr-strict-security.md) está habilitada, incluso si el ensamblado está firmado o la base de datos no está marcada como de confianza.

[ @description =] '*descripción*'  
Descripción de definido por el usuario opcional del ensamblado. Microsoft recomienda usar el nombre canónico que codifica el nombre simple, número de versión, referencia cultural, clave pública y la arquitectura de ensamblado de confianza. Forma exclusiva este valor identifica el ensamblado del lado common language runtime (CLR) y es el mismo que el valor de clr_name en sys.assemblies. 

## <a name="permissions"></a>Permisos

Debe pertenecer a la `sysadmin` rol fijo de servidor o `CONTROL SERVER` permiso.

## <a name="examples"></a>Ejemplos  

En el ejemplo siguiente se agrega un ensamblado denominado `pointudt` a la lista de ensamblados de confianza para el servidor. Estos valores están disponibles en [sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md).     

```  
EXEC sp_add_trusted_assembly 0x8893AD6D78D14EE43DF482E2EAD44123E3A0B684A8873C3F7BF3B5E8D8F09503F3E62370CE742BBC96FE3394477214B84C7C1B0F7A04DCC788FA99C2C09DFCCC, 
N'pointudt, version=0.0.0.0, culture=neutral, publickeytoken=null, processorarchitecture=msil';
```  

## <a name="see-also"></a>Vea también  
  [sys.sp_drop_trusted_assembly](sys-sp-drop-trusted-assembly-transact-sql.md)  
  [sys.trusted_assemblies](../../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md)  
  [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)  
  [Seguridad estricta de CLR](../../database-engine/configure-windows/clr-strict-security.md)  
  [sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)  
  [sys.dm_clr_loaded_assemblies](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)  

