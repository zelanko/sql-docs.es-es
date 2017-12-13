---
title: "Crear una cuenta financiera de dimensión de tipo de elementos primarios y secundarios | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- dimensions [Analysis Services], account
- account dimensions [Analysis Services]
- adding account intelligence
- account intelligence [Analysis Services]
ms.assetid: 2ba74e81-5b4b-407e-acdf-deb2f6accf0a
caps.latest.revision: "15"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a2a38ab84c0ed9dc7b783ec98b2dca2881146584
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="database-dimensions---finance-account-of-parent-child-type"></a>Dimensiones de base de datos - cuenta financiera de tipo de elementos primarios y secundarios
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], una dimensión de tipo de cuenta es una dimensión cuyos atributos representan un gráfico de cuentas para la elaboración de informes financieros.  
  
 Una dimensión de cuenta le permite administrar de forma selectiva el comportamiento de las agregaciones dentro de las cuentas a lo largo del tiempo. Una dimensión de cuenta también permite utilizar un mecanismo estándar para resolver la mayoría de los problemas de agregación no estándar que suelen detectarse en las soluciones de Business Intelligence que procesan datos financieros. Si no se dispone de un mecanismo estándar parecido, para solucionar los problemas de agregación no estándar se necesitan fórmulas de resumen personalizadas, miembros calculados o scripts MDX (Expresiones multidimensionales).  
  
 Para identificar una dimensión como una dimensión de cuenta, establezca la propiedad **Type** de la dimensión en **Accounts**.  
  
## <a name="dimension-structure"></a>Estructura de dimensión  
 Una dimensión de cuenta contiene, como mínimo, dos atributos:  
  
-   Un atributo clave: atributo que identifica las cuentas individuales de la tabla de dimensión para la dimensión de cuenta.  
  
-   Un atributo de cuenta: un atributo superior que describe el modo en que las cuentas se disponen jerárquicamente en la dimensión de cuenta.  
  
     Para identificar un atributo como un atributo de cuenta, establezca la propiedad **Type** del atributo en **Account** y la propiedad **Usage** en **Parent**.  
  
 Las dimensiones de cuenta pueden opcionalmente contener los siguientes atributos:  
  
-   Un atributo de tipo de cuenta: atributo que define el tipo de cuenta de cada cuenta de la dimensión. Los nombres de miembros del atributo de tipo de cuenta se asignan a los tipos de cuenta definidos para la base de datos o proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e indican la función de agregación utilizada por [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para esas cuentas. También pueden utilizarse operadores unarios o fórmulas de resumen personalizadas para determinar el comportamiento de la agregación para los atributos de cuenta, pero los tipos de cuenta permiten aplicar con más facilidad un comportamiento coherente a un gráfico de cuentas sin necesidad de realizar cambios en la base de datos relacional subyacente.  
  
     Para identificar un atributo de tipo de cuenta, establezca la propiedad **Type** del atributo en **AccountType**.  
  
-   Un atributo de nombre de cuenta: atributo que se utiliza para elaborar informes. Para identificar un atributo de nombre de cuenta, establezca la propiedad **Type** del atributo en **AccountName**.  
  
-   Un atributo de número de cuenta: atributo que se utiliza para elaborar informes. Para identificar un atributo de número de cuenta, establezca la propiedad **Type** del atributo en **AccountNumber**.  
  
 Para obtener más información sobre tipos de atributo, vea [Configurar tipos de atributos](../../analysis-services/multidimensional-models/attribute-properties-configure-attribute-types.md).  
  
## <a name="adding-account-intelligence-with-the-business-intelligence-wizard"></a>Agregar inteligencia de cuentas mediante el Asistente de Business Intelligence  
 Tras haber definido una dimensión de cuenta y haber agregado dicha dimensión a un cubo, puede utilizar el Asistente de Business Intelligence para agregar la funcionalidad de inteligencia de cuentas, como, por ejemplo, la asignación de tipos de cuenta, a la dimensión. Para obtener más información, vea [Agregar inteligencia de cuentas a una dimensión](../../analysis-services/multidimensional-models/bi-wizard-add-account-intelligence-to-a-dimension.md).  
  
## <a name="see-also"></a>Vea también  
 [Atributos y jerarquías de atributos](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [Ayuda de F1 de Asistente de Business Intelligence](http://msdn.microsoft.com/library/155ac80c-63ae-47aa-9e86-9396e3d920eb)   
 [Tipos de dimensión](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)  
  
  
