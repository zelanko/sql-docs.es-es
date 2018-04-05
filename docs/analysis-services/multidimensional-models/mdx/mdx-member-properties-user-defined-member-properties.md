---
title: Propiedades de miembro (MDX) definido por el usuario | Documentos de Microsoft
ms.custom: ''
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- custom member properties [MDX]
ms.assetid: b64cc581-e784-42c4-bec8-932abd687423
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 08576f10739533850f04a9e64fa052bf7c6bfeec
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="mdx-member-properties---user-defined-member-properties"></a>Propiedades de miembro MDX - propiedades de miembro definidas por el usuario
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Propiedades de miembro definidas por el usuario pueden agregarse a un determinado con el nombre de nivel en una dimensión como relaciones de atributo. Las propiedades de miembro definidas por el usuario no se pueden agregar al nivel **(Todos)** de una jerarquía ni a la propia jerarquía.  
  
## <a name="creating-user-defined-member-properties"></a>Crear propiedades de miembro definidas por el usuario  
 Las propiedades de miembro definidas por el usuario pueden agregarse a las dimensiones basadas en servidor o a los cubos mediante la interfaz de usuario o mediante programación:  
  
-   Para agregar propiedades de miembro definidas por el usuario en la interfaz de usuario, se usa el Diseñador de dimensiones de [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]. Para obtener más información, vea [Definir relaciones de atributo](../../../analysis-services/multidimensional-models/attribute-relationships-define.md).  
  
-   Para agregar propiedades de miembro definidas por el usuario mediante programación, la aplicación puede utilizar objetos Analysis Manager Objects (AMO) o una combinación de XML for Analysis (XMLA) y Analysis Services Scripting Language (ASSL). Para obtener más información, vea [Relaciones de atributo](../../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md).  
  
## <a name="retrieving-user-defined-member-properties"></a>Recuperar propiedades de miembro definidas por el usuario  
 Para recuperar las propiedades de miembro definidas por el usuario, use la palabra clave **PROPERTIES** o la función [Properties](../../../mdx/properties-mdx.md) .  
  
### <a name="using-the-properties-keyword-to-retrieve-user-defined-member-properties"></a>Usar la palabra clave PROPERTIES para recuperar propiedades de miembro definidas por el usuario  
 La sintaxis para recuperar propiedades de miembro definidas por el usuario es similar a la utilizada para recuperar propiedades de miembro de nivel intrínsecas, como se muestra en el siguiente ejemplo de sintaxis:  
  
 `DIMENSION PROPERTIES [Dimension.]Level.<Custom_Member_Property>`  
  
 La palabra clave **PROPERTIES** aparece después de la expresión de conjuntos de la especificación del eje. Por ejemplo, en la siguiente consulta MDX, la palabra clave **PROPERTIES** recupera las propiedades de miembro definidas por el usuario `List Price` y `Dealer Price` y aparece después de la expresión de conjunto que identifica los productos vendidos en el mes de enero:  
  
```  
SELECT   
   CROSSJOIN([Ship Date].[Calendar].[Calendar Year].Members,   
             [Measures].[Sales Amount]) ON COLUMNS,  
   NON EMPTY Product.Product.MEMBERS  
   DIMENSION PROPERTIES   
              Product.Product.[List Price],  
              Product.Product.[Dealer Price]  ON ROWS  
FROM [Adventure Works]  
WHERE ([Date].[Month of Year].[January])   
```  
  
### <a name="using-the-properties-function-to-retrieve-user-defined-member-properties"></a>Usar la función Properties para recuperar propiedades de miembro definidas por el usuario  
 También puede obtener acceso a las propiedades de miembro personalizado con la función **Properties** . Por ejemplo, la siguiente consulta MDX usa la palabra clave **WITH** para crear un miembro calculado que contiene la propiedad de miembro `List Price`:  
  
```  
WITH   
   MEMBER [Measures].[Product List Price] AS  
   [Product].[Product].CurrentMember.Properties("List Price")  
SELECT   
   [Measures].[Product List Price] on COLUMNS,  
   [Product].[Product].MEMBERS  ON Rows  
FROM [Adventure Works]  
```  
  
 Para obtener más información sobre la creación de miembros calculados, vea [Generar miembros calculados en MDX &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-calculated-members-building-calculated-members.md).  
  
## <a name="see-also"></a>Vea también  
 [Usar las propiedades de miembro &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-member-properties.md)   
 [Propiedades &#40; MDX &#41;](../../../mdx/properties-mdx.md)  
  
  
