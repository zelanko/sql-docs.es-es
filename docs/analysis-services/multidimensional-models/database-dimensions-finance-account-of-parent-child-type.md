---
title: Crear una cuenta financiera de dimensión de tipo de elementos primarios y secundarios | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a9db268d931d46f6254501e95d68739c3e71db3b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "68178870"
---
# <a name="database-dimensions---finance-account-of-parent-child-type"></a>Dimensiones de base de datos: cuenta financiera de tipo de elementos primarios y secundarios
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], una dimensión de tipo cuenta es aquella cuyos atributos representan un gráfico de cuentas para la elaboración de informes financieros.  
  
 Una dimensión de cuenta le permite administrar de forma selectiva el comportamiento de las agregaciones dentro de las cuentas a lo largo del tiempo. Una dimensión de cuenta también permite utilizar un mecanismo estándar para resolver la mayoría de los problemas de agregación no estándar que suelen detectarse en las soluciones de Business Intelligence que procesan datos financieros. Si no se dispone de un mecanismo estándar parecido, para solucionar los problemas de agregación no estándar se necesitan fórmulas de resumen personalizadas, miembros calculados o scripts MDX (Expresiones multidimensionales).  
  
 Para identificar una dimensión como una dimensión de cuenta, establezca la propiedad **Type** de la dimensión en **Accounts**.  
  
## <a name="dimension-structure"></a>Estructura de dimensión  
 Una dimensión de cuenta contiene, como mínimo, dos atributos:  
  
-   Un atributo de un atributo clave que identifica las cuentas individuales de la tabla de dimensiones para la dimensión de cuenta.  
  
-   Un atributo primario de un atributo de cuenta que describe cómo las cuentas se organizan jerárquicamente en la dimensión de cuenta.  
  
     Para identificar un atributo como un atributo de cuenta, establezca la propiedad **Type** del atributo en **Account** y la propiedad **Usage** en **Parent**.  
  
 Las dimensiones de cuenta pueden opcionalmente contener los siguientes atributos:  
  
-   Una cuenta de tipo de atributo de un atributo que define el tipo de cuenta para cada cuenta de la dimensión. Los nombres de miembros del atributo de tipo de cuenta se asignan a los tipos de cuenta definidos para la base de datos o proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e indican la función de agregación utilizada por [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para esas cuentas. También pueden utilizarse operadores unarios o fórmulas de resumen personalizadas para determinar el comportamiento de la agregación para los atributos de cuenta, pero los tipos de cuenta permiten aplicar con más facilidad un comportamiento coherente a un gráfico de cuentas sin necesidad de realizar cambios en la base de datos relacional subyacente.  
  
     Para identificar un atributo de tipo de cuenta, establezca la propiedad **Type** del atributo en **AccountType**.  
  
-   Un nombre atributo un atributo de cuenta que se usa con fines informativos. Para identificar un atributo de nombre de cuenta, establezca la propiedad **Type** del atributo en **AccountName**.  
  
-   Una cuenta del número de atributo de un atributo que se usa con fines informativos. Para identificar un atributo de número de cuenta, establezca la propiedad **Type** del atributo en **AccountNumber**.  
  
 Para obtener más información sobre tipos de atributo, vea [Configurar tipos de atributos](../../analysis-services/multidimensional-models/attribute-properties-configure-attribute-types.md).  
  
## <a name="adding-account-intelligence-with-the-business-intelligence-wizard"></a>Agregar inteligencia de cuentas mediante el Asistente de Business Intelligence  
 Tras haber definido una dimensión de cuenta y haber agregado dicha dimensión a un cubo, puede utilizar el Asistente de Business Intelligence para agregar la funcionalidad de inteligencia de cuentas, como, por ejemplo, la asignación de tipos de cuenta, a la dimensión. Para obtener más información, vea [Agregar inteligencia de cuentas a una dimensión](../../analysis-services/multidimensional-models/bi-wizard-add-account-intelligence-to-a-dimension.md).  
  
## <a name="see-also"></a>Vea también  
 [Atributos y jerarquías de atributos](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [Asistente de Business Intelligence (Ayuda F1)](http://msdn.microsoft.com/library/155ac80c-63ae-47aa-9e86-9396e3d920eb)   
 [Tipos de dimensiones](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)  
  
  
