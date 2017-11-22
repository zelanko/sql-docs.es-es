---
title: "Cambios sustanciales en las características del motor de base de datos de SQL Server 2017 | Microsoft Docs"
description: "Cambios sustanciales en las características del motor de base de datos de SQL Server 2017"
ms.date: 04/19/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: database-engine
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: breaking changes 2017 [SQL Server]
ms.assetid: 
caps.latest.revision: "1"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fd6b58bb3dd8298ced1a04f5b5ba10b960ce776a
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="breaking-changes-to-database-engine-features-in-includesssqlv14-mdincludessssqlv14-mdmd"></a>Cambios sustanciales en las características del motor de base de datos de [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)]
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]


  En este tema se describen cambios importantes introducidos en [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)][!INCLUDE[ssDE](../includes/ssde-md.md)]. Estos cambios pueden provocar errores en las aplicaciones, en los scripts o en las funcionalidades basados en versiones anteriores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Podría encontrar estos problemas al actualizar.  
  
## <a name="breaking-changes-in-includesssqlv14-mdincludessssqlv14-mdmdincludessdeincludesssde-mdmd"></a>Cambios sustanciales en [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)][!INCLUDE[ssDE](../includes/ssde-md.md)]  
  
-  CLR usa la seguridad de acceso del código (CAS) de .NET Framework, que ya no se admite como un límite de seguridad. A partir de [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)], se incluye una opción de `sp_configure` denominada `clr strict security` para mejorar la seguridad de los ensamblados CLR. La opción clr strict security está habilitada de forma predeterminada y trata los ensamblados CLR `SAFE` y `EXTERNAL_ACCESS` como si estuvieran marcados con `UNSAFE`. La opción `clr strict security` se puede deshabilitar para permitir la compatibilidad con versiones anteriores, pero no se recomienda hacerlo. Cuando la opción `clr strict security` está deshabilitada, un ensamblado CLR creado con `PERMISSION_SET = SAFE` puede tener acceso a los recursos externos del sistema, llamar a código no administrado y adquirir privilegios **sysadmin**. Después de habilitar la seguridad estricta, los ensamblados que no estén firmados no podrán cargarse. Además, si una base de datos tiene ensamblados `SAFE` o `EXTERNAL_ACCESS`, las instrucciones `RESTORE` o `ATTACH DATABASE` se completarán, pero los ensamblados no se cargarán.   
  Para cargarlos, debe modificar (o eliminar y volver a crear) cada ensamblado para que se firme con un certificado o clave asimétrica que tenga el inicio de sesión correspondiente con el permiso `UNSAFE ASSEMBLY` en el servidor. Para más información, vea [clr strict security](../database-engine/configure-windows/clr-strict-security.md). 


  
## <a name="previous-versions"></a>Versiones anteriores  

-   [Cambios substanciales en las características del Motor de base de datos de SQL Server 2016](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)  
  
-   [Cambios recientes en las características del Motor de base de datos de SQL Server 2014](https://msdn.microsoft.com/library/ms143179\(v=sql.120\))  
  
-   [Cambios recientes en las características del Motor de base de datos de SQL Server 2012](https://msdn.microsoft.com/library/ms143179\(v=sql.110\))  
  
-   [Cambios recientes en las características del Motor de base de datos de SQL Server 2008](https://msdn.microsoft.com/library/ms143179\(v=sql.100\))  
  
## <a name="see-also"></a>Vea también  
 [Características desusadas del motor de base de datos de SQL Server 2016](../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)   
 [Funcionalidad del motor de base de datos no incluida en SQL Server 2016](../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md)   
 [Compatibilidad con versiones anteriores del Motor de base de datos de SQL Server](../database-engine/sql-server-database-engine-backward-compatibility.md)   
 [Nivel de compatibilidad de ALTER DATABASE &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md)  
  
  
