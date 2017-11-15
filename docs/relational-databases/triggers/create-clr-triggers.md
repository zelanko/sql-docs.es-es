---
title: "Creación de desencadenadores CLR | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-dml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- CRL triggers
- DML triggers, CLR triggers
- DDL triggers, CLR triggers
ms.assetid: 31f41703-134d-49fc-9850-76c297351c2c
caps.latest.revision: "27"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a91a62622569620c0498d5bd0a1fc9c2167b96a9
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="create-clr-triggers"></a>Crear desencadenadores CLR
  Es posible crear un objeto de base de datos dentro de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] programado en un ensamblado creado en Common Language Runtime (CLR) de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] . Los objetos de base de datos que pueden aprovechar el complejo modelo de programación que proporciona CLR incluyen desencadenadores DML, desencadenadores DDL, procedimientos almacenados, funciones, funciones de agregado y tipos.  
  
 Para crear un desencadenador CLR (DML o DDL) en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] siga estos pasos:  
  
-   Defina el desencadenador como una clase en un lenguaje admitido por .NET Framework. Para obtener más información sobre cómo programar desencadenadores en CLR, vea [Desencadenadores CLR](http://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c). A continuación, compile la clase para generar un ensamblado en [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] mediante el compilador del lenguaje adecuado.  
  
-   Registrar el ensamblado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con la instrucción CREATE ASSEMBLY. Para obtener más información sobre ensamblados en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Ensamblados &#40;motor de base de datos&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md).  
  
-   Cree el desencadenador que hace referencia al ensamblado registrado.  
  
> [!NOTE]  
>  La implementación de un proyecto de SQL Server en [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] registra un ensamblado en la base de datos especificada para el proyecto. La implementación del proyecto también crea desencadenadores CLR en la base de datos para todos los métodos anotados con el atributo **SqlTrigger** . Para más información, consulte [Deploying CLR Database Objects](../../relational-databases/clr-integration/deploying-clr-database-objects.md).  
  
> [!NOTE]  
>  La capacidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para ejecutar el código CLR se encuentra desactivada de manera predeterminada. Puede crear, modificar y quitar objetos de base de datos que hacen referencia a los módulos de códigos administrados, pero estas referencias no se ejecutarán en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a menos que se haya habilitado [clr enabled (opción)](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) mediante [sp_configure (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
 **Para crear, modificar o quitar un ensamblado**  
  
-   [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)  
  
-   [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)  
  
-   [DROP ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)  
  
 **Para crear un desencadenador CLR**  
  
-   [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)  
  
## <a name="see-also"></a>Vea también  
 [Desencadenadores DML](../../relational-databases/triggers/dml-triggers.md)   
 [Conceptos de programación en el ámbito de la integración de Common Language Runtime &#40;CLR&#41;](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)   
 [Acceso a datos de objetos de base de datos de CLR](../../relational-databases/clr-integration/data-access/data-access-from-clr-database-objects.md)  
  
  
