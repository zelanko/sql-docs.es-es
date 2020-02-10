---
title: Atributos personalizados para las rutinas CLR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- routines [CLR integration]
- SqlFacet attribute
- SqlTrigger attribute
- SqlProcedure attribute
- custom attributes [CLR integration]
- SqlUserDefinedAggregate attribute
- attributes [CLR integration]
- SqlMethod attribute
- SqlFunction attribute
- common language runtime [SQL Server], attributes
- SqlUserDefinedTypeAttribute attribute
ms.assetid: 95069d22-b05d-4670-b053-15ee2a664e33
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 817591cec64a4210c4cc573588be1b8ac6dfb8a7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62873807"
---
# <a name="custom-attributes-for-clr-routines"></a>Atributos personalizados para las rutinas de CLR
  Los atributos enumerados se pueden aplicar a rutinas Common Language Runtime (CLR), tipos definidos por el usuario y agregados definidos por el usuario que estén [!INCLUDE[msCoName](../../../includes/ssnoversion-md.md)]registrados en. Si no se aplica el atributo, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] asume el valor predeterminado. Los atributos que se enumeran se definen en el espacio de nombres `Microsoft.SqlServer.Server`.  
  
## <a name="the-sqluserdefinedaggregate-attribute"></a>Atributo SqlUserDefinedAggregate  
 El atributo `SqlUserDefinedAggregate` indica que el método debe registrarse como un agregado definido por el usuario. Los agregados definidos por el usuario deben anotarse con este atributo.  
  
 Para obtener más información, vea [SqlUserDefinedAggregateAttribute](https://go.microsoft.com/fwlink/?LinkId=124626).  
  
## <a name="the-sqlfunction-attribute"></a>Atributo SqlFunction  
 El atributo `SqlFunction` indica que el método debe registrarse como una función, con el conjunto de atributos de función correspondiente.  
  
 Para obtener más información, vea [SqlFunctionAttribute](https://go.microsoft.com/fwlink/?LinkId=128019).  
  
## <a name="the-sqlfacet-attribute"></a>Atributo SqlFacet  
 El atributo `SqlFacet` se usa para devolver información acerca del tipo de valor devuelto por una expresión de tipos definidos por el usuario (UDT).  
  
 Para obtener más información, vea [SqlFacetAttribute](https://go.microsoft.com/fwlink/?LinkId=128020).  
  
## <a name="the-sqlprocedure-attribute"></a>Atributo SqlProcedure  
 El atributo `SqlProcedure` indica que el método debe registrarse como un procedimiento almacenado. Solamente Visual Studio usa este atributo para registrar automáticamente el método especificado como un procedimiento almacenado; [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no lo usa.  
  
 Para obtener más información, vea [SqlProcedureAttribute](https://go.microsoft.com/fwlink/?LinkId=128021).  
  
## <a name="the-sqltrigger-attribute"></a>Atributo SqlTrigger  
 El atributo `SqlTrigger` indica que el método debe registrarse como un desencadenador.  
  
 Para obtener más información, vea [SqlTriggerContext](https://go.microsoft.com/fwlink/?LinkId=128022) y [SqlTriggerAttribute](https://go.microsoft.com/fwlink/?LinkId=203898).  
  
## <a name="the-sqluserdefinedtypeattribute"></a>Atributo SqlUserDefinedTypeAttribute  
 Puede aplicar el atributo SqlUserDefinedTypeAttribute a una definición de clase en el ensamblado. Esto hace que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cree un tipo definido por el usuario que se enlaza a la definición de clase que tiene este atributo personalizado.  
  
 Para obtener más información, vea [SqlUserDefinedTypeAttribute](https://go.microsoft.com/fwlink/?LinkId=128024).  
  
## <a name="the-sqlmethod-attribute"></a>Atributo SqlMethod  
 El atributo `SqlMethod` se usa para indicar el determinismo y las propiedades de acceso a datos de un método o una propiedad en un UDT.  
  
 Para obtener más información, vea [SqlMethodAttribute](https://go.microsoft.com/fwlink/?LinkId=128025).  
  
## <a name="see-also"></a>Consulte también  
 [Agregados definidos por el usuario CLR](../../clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md)   
 [Funciones definidas por el usuario de CLR](../../clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)   
 [Tipos definidos por el usuario CLR](../../clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)   
 [Procedimientos almacenados CLR](../../../database-engine/dev-guide/clr-stored-procedures.md)   
 [Desencadenadores CLR](../../../database-engine/dev-guide/clr-triggers.md)  
  
  
