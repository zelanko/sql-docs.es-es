---
title: Instrucción CREATE SET (MDX) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SET
- CREATE SET
- CREATE_SET
- CREATE
dev_langs:
- kbMDX
helpviewer_keywords:
- named sets [MDX]
- CREATE SET statement
ms.assetid: eff51eeb-5e7e-4706-b861-c57b6f3f89f0
caps.latest.revision: 42
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 0b7c9464085c99ff9d04be0c7c6a27d6f216c22b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="mdx-data-definition---create-set"></a>Definición de datos MDX - crear establecido
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Crea un conjunto con nombre con ámbito de sesión para el cubo actual.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CREATE [SESSION] [ STATIC | DYNAMIC ] [HIDDEN] SET   
   CURRENTCUBE | Cube_Name  
      .Set_Name AS 'Set_Expression'  
      [,Property_Name = Property_Value, ...n]  
```  
  
## <a name="arguments"></a>Argumentos  
 *Restricciones obligatorias Cube_Name*  
 Expresión de cadena válida que proporciona el nombre del cubo.  
  
 *Set_Name*  
 Expresión de cadena válida que proporciona el nombre del conjunto con nombre que se va a crear.  
  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Property_name*  
 Cadena válida que proporciona el nombre de una propiedad del conjunto.  
  
 *Property_Value*  
 Expresión escalar válida que define el valor de la propiedad del conjunto.  
  
## <a name="remarks"></a>Comentarios  
 Un conjunto con nombre es un conjunto de miembros de dimensión (o una expresión que define un conjunto) que se crea para utilizarse varias veces. Por ejemplo, un conjunto con nombre posibilita la definición de un conjunto de miembros de dimensión compuesto por el conjunto de los diez establecimientos con más ventas. Este conjunto puede definirse de forma estática o mediante una función como [TopCount](../mdx/topcount-mdx.md). Este conjunto con nombre puede usarse cuando se necesite el conjunto de los diez mejores establecimientos.  
  
 La instrucción CREATE SET crea un conjunto con nombre que permanece disponible durante toda la sesión, y por lo tanto, puede usarse en diversas consultas durante una sesión. Para obtener más información, consulte [miembros calculados de Creating Session-Scoped &#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/mdx-calculated-members-session-scoped-calculated-members.md).  
  
 También puede definir un conjunto con nombre para que lo use una sola consulta. Para definir un conjunto de este tipo, utilice la cláusula WITH en la instrucción SELECT. Para obtener más información acerca de la cláusula WITH, consulte [conjuntos con nombre de Creating Query-Scoped &#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/mdx-named-sets-creating-query-scoped-named-sets.md).  
  
 El *función* cláusula puede contener cualquier función que admite la sintaxis MDX. Los conjuntos creados con la instrucción CREATE SET que no especifiquen la cláusula SESSION tienen ámbito de sesión. Utilice la cláusula WITH para crear un conjunto con ámbito de consulta.  
  
 Si especifica un cubo distinto del que está conectado actualmente, se genera un error. Por lo tanto, debe utilizar CURRENTCUBE en lugar de un nombre de cubo para indicar el cubo actual.  
  
## <a name="scope"></a>Ámbito  
 Un conjunto definido pro el usuario puede producirse en uno de los ámbitos enumerados en la tabla siguiente.  
  
 Ámbito de consulta  
 La visibilidad y duración del conjunto se limita a la consulta. El conjunto se define en una consulta individual. El ámbito de consulta prevalece sobre el ámbito de sesión. Para obtener más información, consulte [conjuntos con nombre de Creating Query-Scoped &#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/mdx-named-sets-creating-query-scoped-named-sets.md).  
  
 Ámbito de sesión  
 La visibilidad y duración del conjunto se limita a la sesión en la que se creó. (La duración es menor que la duración de la sesión si se emite una instrucción DROP SET en el conjunto.) La instrucción CREATE SET crea un conjunto con ámbito de sesión. Utilice la cláusula WITH para crear un conjunto con ámbito de consulta.  
  
### <a name="example"></a>Ejemplo  
 El siguiente ejemplo crea un conjunto denominado Core Products. A continuación, la consulta SELECT llama al conjunto recién creado. La instrucción CREATE SET debe ejecutarse antes de que se pueda ejecutar la consulta SELECT (no se pueden ejecutar en el mismo lote).  
  
```  
CREATE SET [Adventure Works].[Core Products] AS '{[Product].[Category].[Bikes]}'  
  
SELECT [Core Products] ON 0  
  FROM [Adventure Works]  
```  
  
## <a name="set-evaluation"></a>Evaluación del conjunto  
 La evaluación del conjunto se puede programar para producirse de manera diferente; se puede definir para que se produzca solo una vez cuando se crea el conjunto o cada vez que se utilice el conjunto.  
  
 STATIC  
 Indica que el conjunto solo se evalúa una vez cuando se evalúa la instrucción CREATE SET.  
  
 DYNAMIC  
 Indica que el conjunto se evaluará cada vez que se use en una consulta.  
  
## <a name="set-visibility"></a>Visibilidad del conjunto  
 El conjunto puede estar o visible o no para otros usuarios que consultan el cubo.  
  
 HIDDEN  
 Especifica que el conjunto no está visible para los usuarios que consultan el cubo.  
  
## <a name="standard-properties"></a>Propiedades estándar  
 Cada conjunto tiene una serie de propiedades predeterminadas. Cuando una aplicación cliente está conectada a [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], las propiedades predeterminadas son compatibles o disponibles para ser compatibles, como el administrador elige.  
  
|Identificador de la propiedad|Significado|  
|-------------------------|-------------|  
|CAPTION|Cadena que utiliza la aplicación cliente como título para el conjunto.|  
|DISPLAY_FOLDER|Cadena que identifica la ruta de la carpeta que usa la aplicación cliente para mostrar el conjunto. La aplicación cliente define el separador de niveles de carpetas. Para las herramientas y clientes proporcionados por [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], la barra diagonal inversa (\\) es el separador de niveles. Si va a asignar varias carpetas para mostrar a un conjunto definido, utilice un punto y coma (;) para separar las carpetas.|  
  
## <a name="see-also"></a>Vea también  
 [Instrucción de conjunto de DROP &#40;MDX&#41;](../mdx/mdx-data-definition-drop-set.md)   
 [Instrucciones de definición de datos MDX &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
