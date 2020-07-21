---
title: Creación de funciones de agregado definidas por el usuario | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- aggregate functions [SQL Server], user-defined
- user-defined functions [CLR integration]
ms.assetid: c278b746-6323-4b32-b460-239915acc067
author: rothja
ms.author: jroth
ms.openlocfilehash: d66db5586f5f80f8f0e8954d041befbcd4c5eba4
ms.sourcegitcommit: 703968b86a111111a82ef66bb7467dbf68126051
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/07/2020
ms.locfileid: "86053641"
---
# <a name="create-user-defined-aggregates"></a>Crear funciones de agregado definidas por el usuario
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]
  Es posible crear en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] un objeto de base de datos programado en un ensamblado CLR. Los objetos de base de datos que pueden aprovechar el completo modelo de programación que proporciona CLR incluyen desencadenadores, procedimientos almacenados, funciones, funciones de agregado y tipos.  
  
 Al igual que las funciones de agregado integradas que proporciona [!INCLUDE[tsql](../../includes/tsql-md.md)], las funciones de agregado definidas por el usuario realizan un cálculo en un conjunto de valores y devuelven un único valor.  
  
 La creación de una función de agregado definida por el usuario en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] implica estos pasos:  
  
-   Establecer la función de agregado definida por el usuario como una clase en un lenguaje de [!INCLUDE[msCoName](../../includes/msconame-md.md)] compatible con .NET Framework. Para obtener más información sobre cómo programar funciones de agregado definidas por el usuario en CRL, vea [Agregados definidos por el usuario de CLR](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md). Compile esta clase para generar un ensamblado CRL con el compilador de lenguaje correspondiente.  
  
-   Registrar el ensamblado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con la instrucción CREATE ASSEMBLY. Para obtener más información sobre ensamblados en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Ensamblados &#40;motor de base de datos&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md).  
  
-   Crear la función de agregado definida por el usuario que hace referencia al ensamblado registrado con la instrucción CREATE AGGREGATE.  
  
> [!NOTE]
>  La implementación de un proyecto de SQL Server en [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] registra un ensamblado en la base de datos especificada para el proyecto. La implementación del proyecto también crea un agregado definido por el usuario en la base de datos para todas las definiciones de clase anotadas con el atributo **SqlUserDefinedAggregate** . Para más información, consulte [Deploying CLR Database Objects](../../relational-databases/clr-integration/deploying-clr-database-objects.md).  
> 
> [!NOTE]
>  La capacidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para ejecutar el código CLR se encuentra desactivada de manera predeterminada. Puede crear, modificar y quitar objetos de base de datos que hacen referencia a los módulos de códigos administrados; pero, estas referencias no se ejecutarán en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a menos que se haya habilitado la opción [clr enabled Option](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) por medio de [sp_configure (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
 **Para crear, modificar o quitar un ensamblado**  
  
-   [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)  
  
-   [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)  
  
-   [DROP ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)  
  
 **Para crear una función de agregado definida por el usuario**  
  
-   [CREATE AGGREGATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-aggregate-transact-sql.md)  
  
## <a name="see-also"></a>Consulte también  
 [Conceptos de programación en el ámbito de la integración de Common Language Runtime &#40;CLR&#41;](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  
  
  
