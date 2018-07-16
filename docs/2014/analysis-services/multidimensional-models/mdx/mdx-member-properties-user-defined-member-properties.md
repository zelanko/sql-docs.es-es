---
title: Propiedades de miembro (MDX) definido por el usuario | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- custom member properties [MDX]
ms.assetid: b64cc581-e784-42c4-bec8-932abd687423
caps.latest.revision: 33
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 50af6373446859ac0bf98a7170504b9d58c4a5f9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37321285"
---
# <a name="user-defined-member-properties-mdx"></a>Propiedades de miembro definidas por el usuario (MDX)
  Las propiedades de miembro definidas por el usuario se pueden agregar a un nivel con nombre específico de una dimensión como relaciones de atributo. Las propiedades de miembro definidas por el usuario no pueden agregarse a la `(All)` nivel de una jerarquía o a la propia jerarquía.  
  
## <a name="creating-user-defined-member-properties"></a>Crear propiedades de miembro definidas por el usuario  
 Las propiedades de miembro definidas por el usuario pueden agregarse a las dimensiones basadas en servidor o a los cubos mediante la interfaz de usuario o mediante programación:  
  
-   Para agregar propiedades de miembro definidas por el usuario en la interfaz de usuario, se usa el Diseñador de dimensiones de [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]. Para obtener más información, vea [Definir relaciones de atributo](../attribute-relationships-define.md).  
  
-   Para agregar propiedades de miembro definidas por el usuario mediante programación, la aplicación puede utilizar objetos Analysis Manager Objects (AMO) o una combinación de XML for Analysis (XMLA) y Analysis Services Scripting Language (ASSL). Para obtener más información, vea [Relaciones de atributo](../../multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md).  
  
## <a name="retrieving-user-defined-member-properties"></a>Recuperar propiedades de miembro definidas por el usuario  
 Puede recuperar las propiedades de miembro definidas por el usuario mediante el `PROPERTIES` palabra clave o el [propiedades](/sql/mdx/properties-mdx) función.  
  
### <a name="using-the-properties-keyword-to-retrieve-user-defined-member-properties"></a>Usar la palabra clave PROPERTIES para recuperar propiedades de miembro definidas por el usuario  
 La sintaxis para recuperar propiedades de miembro definidas por el usuario es similar a la utilizada para recuperar propiedades de miembro de nivel intrínsecas, como se muestra en el siguiente ejemplo de sintaxis:  
  
 `DIMENSION PROPERTIES [Dimension.]Level.<Custom_Member_Property>`  
  
 El `PROPERTIES` palabra clave aparece después de la expresión de conjunto de la especificación del eje. Por ejemplo, la siguiente consulta MDX el `PROPERTIES` palabra clave se recupera la `List Price` y `Dealer Price` las propiedades de miembro definidas por el usuario y aparece después de la expresión de conjunto que identifica los productos vendidos en enero:  
  
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
 También puede obtener acceso a las propiedades de miembro personalizado con la función `Properties`. Por ejemplo, la siguiente consulta MDX utiliza la `WITH` palabra clave para crear un miembro calculado que consta de los `List Price` propiedad de miembro:  
  
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
 [Uso de las propiedades de miembro &#40;MDX&#41;](mdx-member-properties.md)   
 [Propiedades &#40;MDX&#41;](/sql/mdx/properties-mdx)  
  
  
