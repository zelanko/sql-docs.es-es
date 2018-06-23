---
title: Propiedades de miembro (MDX) definido por el usuario | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- custom member properties [MDX]
ms.assetid: b64cc581-e784-42c4-bec8-932abd687423
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: ba34243609b796eef635fc3b55cd99ef4f225638
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107054"
---
# <a name="user-defined-member-properties-mdx"></a>Propiedades de miembro definidas por el usuario (MDX)
  Las propiedades de miembro definidas por el usuario se pueden agregar a un nivel con nombre específico de una dimensión como relaciones de atributo. Propiedades de miembro definidas por el usuario no puede agregarse a la `(All)` nivel de una jerarquía o a la propia jerarquía.  
  
## <a name="creating-user-defined-member-properties"></a>Crear propiedades de miembro definidas por el usuario  
 Las propiedades de miembro definidas por el usuario pueden agregarse a las dimensiones basadas en servidor o a los cubos mediante la interfaz de usuario o mediante programación:  
  
-   Para agregar propiedades de miembro definidas por el usuario en la interfaz de usuario, se usa el Diseñador de dimensiones de [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]. Para obtener más información, vea [Definir relaciones de atributo](../attribute-relationships-define.md).  
  
-   Para agregar propiedades de miembro definidas por el usuario mediante programación, la aplicación puede utilizar objetos Analysis Manager Objects (AMO) o una combinación de XML for Analysis (XMLA) y Analysis Services Scripting Language (ASSL). Para obtener más información, vea [Relaciones de atributo](../../multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md).  
  
## <a name="retrieving-user-defined-member-properties"></a>Recuperar propiedades de miembro definidas por el usuario  
 Puede recuperar las propiedades de miembro definidas por el usuario mediante el `PROPERTIES` palabra clave o el [propiedades](/sql/mdx/properties-mdx) función.  
  
### <a name="using-the-properties-keyword-to-retrieve-user-defined-member-properties"></a>Usar la palabra clave PROPERTIES para recuperar propiedades de miembro definidas por el usuario  
 La sintaxis para recuperar propiedades de miembro definidas por el usuario es similar a la utilizada para recuperar propiedades de miembro de nivel intrínsecas, como se muestra en el siguiente ejemplo de sintaxis:  
  
 `DIMENSION PROPERTIES [Dimension.]Level.<Custom_Member_Property>`  
  
 El `PROPERTIES` palabra clave aparece después de la expresión de conjunto de la especificación del eje. Por ejemplo, la siguiente consulta MDX la `PROPERTIES` palabra clave recupera la `List Price` y `Dealer Price` propiedades de miembro definidas por el usuario y aparece después de la expresión de conjunto que identifica los productos vendidos en enero:  
  
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
 También puede obtener acceso a las propiedades de miembro personalizado con la función `Properties`. Por ejemplo, la siguiente consulta MDX utiliza la `WITH` palabra clave que se va a crear un miembro calculado que consta de los `List Price` propiedad de miembro:  
  
```  
WITH   
   MEMBER [Measures].[Product List Price] AS  
   [Product].[Product].CurrentMember.Properties("List Price")  
SELECT   
   [Measures].[Product List Price] on COLUMNS,  
   [Product].[Product].MEMBERS  ON Rows  
FROM [Adventure Works]  
```  
  
 Para obtener más información sobre la creación de miembros calculados, vea [Generar miembros calculados en MDX &#40;MDX&#41;](mdx-calculated-members-building-calculated-members.md).  
  
## <a name="see-also"></a>Vea también  
 [Mediante las propiedades de miembro &#40;MDX&#41;](mdx-member-properties.md)   
 [Propiedades &#40;MDX&#41;](/sql/mdx/properties-mdx)  
  
  
