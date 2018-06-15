---
title: Atributos personalizados para las rutinas CLR | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
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
ms.openlocfilehash: f5672efbc82371c5447fc927b208e41efad20d2d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32924670"
---
# <a name="clr-integration-custom-attributes-for-clr-routines"></a>Atributos personalizados de integración de CLR rutinas CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Los atributos que aparecen pueden aplicarse a rutinas de runtime (CLR) de lenguaje común, tipos definidos por el usuario y agregados definidos por el usuario que están registrados en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Si no se aplica el atributo, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] asume el valor predeterminado. Se definen los atributos que aparecen en la **Microsoft.SqlServer.Server** espacio de nombres.  
  
## <a name="the-sqluserdefinedaggregate-attribute"></a>Atributo SqlUserDefinedAggregate  
 El **SqlUserDefinedAggregate** atributo indica que el método debe registrarse como un agregado definido por el usuario. Los agregados definidos por el usuario deben anotarse con este atributo.  
  
 Para obtener más información, consulte [SqlUserDefinedAggregateAttribute](http://go.microsoft.com/fwlink/?LinkId=124626).  
  
## <a name="the-sqlfunction-attribute"></a>Atributo SqlFunction  
 El **SqlFunction** atributo indica que el método debe registrarse como una función, con el conjunto de atributos de función correspondiente.  
  
 Para obtener más información, consulte [SqlFunctionAttribute](http://go.microsoft.com/fwlink/?LinkId=128019).  
  
## <a name="the-sqlfacet-attribute"></a>Atributo SqlFacet  
 El **SqlFacet** atributo se utiliza para devolver información sobre el tipo de valor devuelto de una expresión de tipo definido por el usuario (UDT).  
  
 Para obtener más información, consulte [SqlFacetAttribute](http://go.microsoft.com/fwlink/?LinkId=128020).  
  
## <a name="the-sqlprocedure-attribute"></a>Atributo SqlProcedure  
 El **SqlProcedure** atributo indica que el método debe registrarse como un procedimiento almacenado. Solamente Visual Studio usa este atributo para registrar automáticamente el método especificado como un procedimiento almacenado; [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no lo usa.  
  
 Para obtener más información, consulte [SqlProcedureAttribute](http://go.microsoft.com/fwlink/?LinkId=128021).  
  
## <a name="the-sqltrigger-attribute"></a>Atributo SqlTrigger  
 El **SqlTrigger** atributo indica que el método debe registrarse como un desencadenador.  
  
 Para obtener más información, consulte [SqlTriggerContext](http://go.microsoft.com/fwlink/?LinkId=128022) y [SqlTriggerAttribute](http://go.microsoft.com/fwlink/?LinkId=203898).  
  
## <a name="the-sqluserdefinedtypeattribute"></a>Atributo SqlUserDefinedTypeAttribute  
 Puede aplicar el atributo SqlUserDefinedTypeAttribute a una definición de clase en el ensamblado. Esto hace que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cree un tipo definido por el usuario que se enlaza a la definición de clase que tiene este atributo personalizado.  
  
 Para obtener más información, consulte [SqlUserDefinedTypeAttribute](http://go.microsoft.com/fwlink/?LinkId=128024).  
  
## <a name="the-sqlmethod-attribute"></a>Atributo SqlMethod  
 El **SqlMethod** atributo se utiliza para indicar las propiedades de acceso a datos y determinismo de un método o una propiedad en un UDT.  
  
 Para obtener más información, consulte [SqlMethodAttribute](http://go.microsoft.com/fwlink/?LinkId=128025).  
  
## <a name="see-also"></a>Vea también  
 [Agregados definidos por el usuario CLR](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md)   
 [Funciones definidas por el usuario CLR](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)   
 [Tipos definidos por el usuario CLR](../../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)   
 [Procedimientos almacenados de CLR](http://msdn.microsoft.com/library/bbdd51b2-a9b4-4916-ba6f-7957ac6c3f33)   
 [Desencadenadores CLR](http://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)  
  
  
