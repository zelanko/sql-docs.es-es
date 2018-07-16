---
title: Los atributos personalizados para las rutinas CLR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: clr
ms.tgt_pltfrm: ''
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
caps.latest.revision: 82
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a2f3e1980c164327e584d8f485c2d08571534245
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37351047"
---
# <a name="custom-attributes-for-clr-routines"></a>Atributos personalizados para las rutinas de CLR
  Los atributos listados pueden aplicarse a rutinas de common language runtime (CLR), tipos definidos por el usuario y agregados definidos por el usuario que están registrados en [!INCLUDE[msCoName](../../../includes/ssnoversion-md.md)]. Si no se aplica el atributo, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] asume el valor predeterminado. Los atributos que se enumeran se definen en el espacio de nombres `Microsoft.SqlServer.Server`.  
  
## <a name="the-sqluserdefinedaggregate-attribute"></a>Atributo SqlUserDefinedAggregate  
 El atributo `SqlUserDefinedAggregate` indica que el método debe registrarse como un agregado definido por el usuario. Los agregados definidos por el usuario deben anotarse con este atributo.  
  
 Para obtener más información, consulte [SqlUserDefinedAggregateAttribute](http://go.microsoft.com/fwlink/?LinkId=124626).  
  
## <a name="the-sqlfunction-attribute"></a>Atributo SqlFunction  
 El atributo `SqlFunction` indica que el método debe registrarse como una función, con el conjunto de atributos de función correspondiente.  
  
 Para obtener más información, consulte [SqlFunctionAttribute](http://go.microsoft.com/fwlink/?LinkId=128019).  
  
## <a name="the-sqlfacet-attribute"></a>Atributo SqlFacet  
 El atributo `SqlFacet` se usa para devolver información acerca del tipo de valor devuelto por una expresión de tipos definidos por el usuario (UDT).  
  
 Para obtener más información, consulte [SqlFacetAttribute](http://go.microsoft.com/fwlink/?LinkId=128020).  
  
## <a name="the-sqlprocedure-attribute"></a>Atributo SqlProcedure  
 El atributo `SqlProcedure` indica que el método debe registrarse como un procedimiento almacenado. Solamente Visual Studio usa este atributo para registrar automáticamente el método especificado como un procedimiento almacenado; [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no lo usa.  
  
 Para obtener más información, consulte [SqlProcedureAttribute](http://go.microsoft.com/fwlink/?LinkId=128021).  
  
## <a name="the-sqltrigger-attribute"></a>Atributo SqlTrigger  
 El atributo `SqlTrigger` indica que el método debe registrarse como un desencadenador.  
  
 Para obtener más información, consulte [SqlTriggerContext](http://go.microsoft.com/fwlink/?LinkId=128022) y [SqlTriggerAttribute](http://go.microsoft.com/fwlink/?LinkId=203898).  
  
## <a name="the-sqluserdefinedtypeattribute"></a>Atributo SqlUserDefinedTypeAttribute  
 Puede aplicar el atributo SqlUserDefinedTypeAttribute a una definición de clase en el ensamblado. Esto hace que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cree un tipo definido por el usuario que se enlaza a la definición de clase que tiene este atributo personalizado.  
  
 Para obtener más información, consulte [SqlUserDefinedTypeAttribute](http://go.microsoft.com/fwlink/?LinkId=128024).  
  
## <a name="the-sqlmethod-attribute"></a>Atributo SqlMethod  
 El atributo `SqlMethod` se usa para indicar el determinismo y las propiedades de acceso a datos de un método o una propiedad en un UDT.  
  
 Para obtener más información, consulte [SqlMethodAttribute](http://go.microsoft.com/fwlink/?LinkId=128025).  
  
## <a name="see-also"></a>Vea también  
 [Agregados definidos por el usuario CLR](../../clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md)   
 [CLR User-Defined Functions](../../clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)  (Funciones definidas por el usuario CLR)  
 [Tipos definidos por el usuario CLR](../../clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)   
 [Procedimientos almacenados de CLR](../../../database-engine/dev-guide/clr-stored-procedures.md)   
 [Desencadenadores CLR](../../../database-engine/dev-guide/clr-triggers.md)  
  
  
