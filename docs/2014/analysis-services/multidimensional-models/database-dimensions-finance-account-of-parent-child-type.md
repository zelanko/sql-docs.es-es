---
title: Crear una cuenta financiera de una dimensión de tipo primario-secundario | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- dimensions [Analysis Services], account
- account dimensions [Analysis Services]
- adding account intelligence
- account intelligence [Analysis Services]
ms.assetid: 2ba74e81-5b4b-407e-acdf-deb2f6accf0a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 28a7cf6b3a712144daead54d521fb3cc6936c99e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66075921"
---
# <a name="create-a-finance-account-of-parent-child-type-dimension"></a>Crear una cuenta financiera de una dimensión de tipo primario-secundario
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] En [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], una dimensión de tipo cuenta es una dimensión cuyos atributos representan un gráfico de cuentas para la elaboración de informes financieros.  
  
 Una dimensión de cuenta le permite administrar de forma selectiva el comportamiento de las agregaciones dentro de las cuentas a lo largo del tiempo. Una dimensión de cuenta también permite utilizar un mecanismo estándar para resolver la mayoría de los problemas de agregación no estándar que suelen detectarse en las soluciones de Business Intelligence que procesan datos financieros. Si no se dispone de un mecanismo estándar parecido, para solucionar los problemas de agregación no estándar se necesitan fórmulas de resumen personalizadas, miembros calculados o scripts MDX (Expresiones multidimensionales).  
  
 Para identificar una dimensión como una dimensión de cuenta, establezca la propiedad `Type` de la dimensión en `Accounts`.  
  
## <a name="dimension-structure"></a>Estructura de dimensión  
 Una dimensión de cuenta contiene, como mínimo, dos atributos:  
  
-   Un atributo clave: atributo que identifica las cuentas individuales de la tabla de dimensiones para la dimensión de cuenta.  
  
-   Un atributo de cuenta: un atributo primario que describe el modo en que las cuentas se organizan jerárquicamente en la dimensión de cuenta.  
  
     Para identificar un atributo como un atributo de cuenta, establezca la propiedad `Type` del atributo en `Account` y la propiedad `Usage` en `Parent`.  
  
 Las dimensiones de cuenta pueden opcionalmente contener los siguientes atributos:  
  
-   Un atributo de tipo de cuenta: un atributo que define el tipo de cuenta de cada cuenta de la dimensión. Los nombres de miembros del atributo de tipo de cuenta se asignan a los tipos de cuenta definidos para la base de datos o proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e indican la función de agregación utilizada por [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para esas cuentas. También pueden utilizarse operadores unarios o fórmulas de resumen personalizadas para determinar el comportamiento de la agregación para los atributos de cuenta, pero los tipos de cuenta permiten aplicar con más facilidad un comportamiento coherente a un gráfico de cuentas sin necesidad de realizar cambios en la base de datos relacional subyacente.  
  
     Para identificar un atributo de tipo de cuenta, establezca la propiedad `Type` del atributo en `AccountType`.  
  
-   Un atributo de nombre de cuenta: atributo que se utiliza para la elaboración de informes. Para identificar un atributo de nombre de cuenta, establezca la propiedad `Type` del atributo en `AccountName`.  
  
-   Un atributo de número de cuenta: atributo que se utiliza para la elaboración de informes. Para identificar un atributo de número de cuenta, establezca la propiedad `Type` del atributo en `AccountNumber`.  
  
 Para obtener más información sobre tipos de atributo, vea [Configurar tipos de atributos](attribute-properties-configure-attribute-types.md).  
  
## <a name="adding-account-intelligence-with-the-business-intelligence-wizard"></a>Agregar inteligencia de cuentas mediante el Asistente de Business Intelligence  
 Tras haber definido una dimensión de cuenta y haber agregado dicha dimensión a un cubo, puede utilizar el Asistente de Business Intelligence para agregar la funcionalidad de inteligencia de cuentas, como, por ejemplo, la asignación de tipos de cuenta, a la dimensión. Para obtener más información, vea [Agregar inteligencia de cuentas a una dimensión](bi-wizard-add-account-intelligence-to-a-dimension.md).  
  
## <a name="see-also"></a>Consulte también  
 [Atributos y jerarquías de atributos](../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [Asistente de Business Intelligence (ayuda F1)](../business-intelligence-wizard-f1-help.md)   
 [Tipos de dimensiones](../multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)  
  
  
