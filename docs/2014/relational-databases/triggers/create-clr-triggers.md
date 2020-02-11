---
title: Creación de desencadenadores CLR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- CRL triggers
- DML triggers, CLR triggers
- DDL triggers, CLR triggers
ms.assetid: 31f41703-134d-49fc-9850-76c297351c2c
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b68531b962b10785927c6212b2483f2d9c1d7d3a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62698828"
---
# <a name="create-clr-triggers"></a>Crear desencadenadores CLR
  Puede crear un objeto de base de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos dentro de programado en un ensamblado creado [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] en el Common Language Runtime (CLR). Los objetos de base de datos que pueden aprovechar el complejo modelo de programación que proporciona CLR incluyen desencadenadores DML, desencadenadores DDL, procedimientos almacenados, funciones, funciones de agregado y tipos.  
  
 Para crear un desencadenador CLR (DML o DDL) en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] siga estos pasos:  
  
-   Defina el desencadenador como una clase en un lenguaje admitido por .NET Framework. Para obtener más información sobre cómo programar desencadenadores en CLR, vea [Desencadenadores CLR](../../database-engine/dev-guide/clr-triggers.md). A continuación, compile la clase para generar un ensamblado en [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] mediante el compilador del lenguaje adecuado.  
  
-   Registrar el ensamblado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con la instrucción CREATE ASSEMBLY. Para obtener más información sobre ensamblados en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Ensamblados &#40;motor de base de datos&#41;](../clr-integration/assemblies-database-engine.md).  
  
-   Cree el desencadenador que hace referencia al ensamblado registrado.  
  
> [!NOTE]  
>  La implementación de un proyecto de SQL Server en [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] registra un ensamblado en la base de datos especificada para el proyecto. La implementación del proyecto también crea desencadenadores CLR en la base de datos para todos los métodos anotados con el atributo `SqlTrigger`. Para más información, consulte [Deploying CLR Database Objects](../clr-integration/deploying-clr-database-objects.md).  
  
> [!NOTE]  
>  La capacidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para ejecutar el código CLR se encuentra desactivada de manera predeterminada. Puede crear, modificar y quitar objetos de base de datos que hagan referencia a módulos de código administrado, pero estas referencias [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se ejecutarán en a menos que se habilite la [opción clr enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) mediante [sp_configure (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql).  
  
 **Para crear, modificar o quitar un ensamblado**  
  
-   [CREATE ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-assembly-transact-sql)  
  
-   [ALTER ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-assembly-transact-sql)  
  
-   [DROP ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-assembly-transact-sql)  
  
 **Para crear un desencadenador CLR**  
  
-   [CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql)  
  
## <a name="see-also"></a>Consulte también  
 [Desencadenadores DML](dml-triggers.md)   
 [Conceptos de programación de la integración de Common Language Runtime &#40;CLR&#41;](../clr-integration/common-language-runtime-clr-integration-programming-concepts.md)   
 [Acceso a datos de objetos de base de datos de CLR](../clr-integration/data-access/data-access-from-clr-database-objects.md)  
  
  
