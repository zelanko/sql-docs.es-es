---
title: Cambios sustanciales en las características del motor de base de datos de SQL Server 2017 | Microsoft Docs
description: Cambios sustanciales en las características del motor de base de datos de SQL Server 2017
ms.date: 11/27/2018
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.custom: ''
ms.technology: release-landing
ms.topic: conceptual
helpviewer_keywords:
- breaking changes 2017 [SQL Server]
ms.assetid: ''
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 61fb2e329b60468ece3f87eeacefb7490908dba4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66802578"
---
# <a name="breaking-changes-to-database-engine-features-in-includesssqlv14-mdincludessssqlv14-mdmd"></a>Cambios sustanciales en las características del motor de base de datos de [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)]
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]


  En este tema se describen cambios importantes introducidos en [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)]. Estos cambios pueden provocar errores en las aplicaciones, en los scripts o en las funcionalidades basados en versiones anteriores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Podría encontrar estos problemas al actualizar.  
  
## <a name="breaking-changes-in-includesssqlv14-mdincludessssqlv14-mdmd-includessdeincludesssde-mdmd"></a>Cambios importantes in [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)]  
  
-  CLR usa la seguridad de acceso del código (CAS) de .NET Framework, que ya no se admite como un límite de seguridad. A partir de [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)], se incluye una opción de `sp_configure` denominada `clr strict security` para mejorar la seguridad de los ensamblados CLR. La opción clr strict security está habilitada de forma predeterminada y trata los ensamblados CLR `SAFE` y `EXTERNAL_ACCESS` como si estuvieran marcados con `UNSAFE`. La opción `clr strict security` se puede deshabilitar para permitir la compatibilidad con versiones anteriores, pero no se recomienda hacerlo. Cuando la opción `clr strict security` está deshabilitada, un ensamblado CLR creado con `PERMISSION_SET = SAFE` puede tener acceso a los recursos externos del sistema, llamar a código no administrado y adquirir privilegios **sysadmin**. Después de habilitar la seguridad estricta, los ensamblados que no estén firmados no podrán cargarse. Además, si una base de datos tiene ensamblados `SAFE` o `EXTERNAL_ACCESS`, las instrucciones `RESTORE` o `ATTACH DATABASE` se completarán, pero los ensamblados no se cargarán.   
  Para cargarlos, debe modificar (o eliminar y volver a crear) cada ensamblado para que se firme con un certificado o clave asimétrica que tenga el inicio de sesión correspondiente con el permiso `UNSAFE ASSEMBLY` en el servidor. Para obtener más información, vea [CLR strict security](../database-engine/configure-windows/clr-strict-security.md). 

## <a name="previous-versions"></a> Versiones anteriores  

- [Cambios substanciales en las características del Motor de base de datos de SQL Server 2016](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)

- [Cambios recientes en las características del Motor de base de datos de SQL Server 2014](https://docs.microsoft.com/sql/database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016?view=sql-server-2014#SQL14)

#### <a name="archived-documentation-for-very-old-versions-of-sql-server"></a>Documentación archivada para las versiones muy antiguas de SQL Server

[!INCLUDE[Archived documentation for very old versions of SQL Server](../includes/paragraph-content/previous-versions-archive-documentation-sql-server.md)]

## <a name="see-also"></a>Consulte también  
 [Características desusadas del motor de base de datos de SQL Server 2016](../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)   
 [Funcionalidad del motor de base de datos no incluida en SQL Server 2016](../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md)   
 [Compatibilidad con versiones anteriores del Motor de base de datos de SQL Server](../database-engine/sql-server-database-engine-backward-compatibility.md)   
 [Nivel de compatibilidad de ALTER DATABASE &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md)  
  
  
