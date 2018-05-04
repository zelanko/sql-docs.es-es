---
title: Instrucción UPDATE MEMBER (MDX) | Documentos de Microsoft
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
- UPDATE_MEMBER
- UPDATE MEMBER
- MEMBER
- UPDATE
helpviewer_keywords:
- calculated members [MDX]
- UPDATE MEMBER statement
ms.assetid: 07ab708d-d165-4fb1-a9f9-fb8197ff0dab
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 6f5591eeaaa2afd346e8038426f72e9b0c21520c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="mdx-data-definition---update-member"></a>Definición de datos MDX - UPDATE MEMBER
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Actualiza un miembro calculado existente.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
UPDATE MEMBER Cube_Name.Member_Name   
   AS MDX_Expression  
      [,Property_Name = Property_Value, ...n]  
......[,SCOPE_ISOLATION = CUBE]  
```  
  
## <a name="arguments"></a>Argumentos  
 *Restricciones obligatorias Cube_Name*  
 Expresión de cadena válida que especifica el nombre del cubo que contiene el miembro.  
  
 *Member_Name*  
 Expresión de cadena válida que especifica el nombre de un miembro existente.  
  
 *MDX_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida a la que se va a actualizar el miembro.  
  
 *Property_name*  
 Cadena válida que especifica el nombre de una propiedad de miembro calculado.  
  
 *Property_Value*  
 Expresión escalar válida que especifica el valor de la propiedad para el miembro calculado.  
  
## <a name="remarks"></a>Comentarios  
 La instrucción UPDATE MEMBER actualiza un miembro calculado existente conservando la prioridad relativa de este miembro con respecto a otros cálculos. Por consiguiente, no puede utilizar la instrucción UPDATE MEMBER para cambiar SOLVEORDER.  
  
 Una instrucción UPDATE MEMBER no se puede especificar en el script MDX para un cubo.  
  
 Si especifica un cubo distinto del que está conectado actualmente, se genera un error. Por lo tanto, debe utilizar CURRENTCUBE en lugar de un nombre de cubo para indicar el cubo actual.  
  
 Para obtener más información acerca de las propiedades de miembro definidas por OLE DB, vea la documentación de OLE DB.  
  
## <a name="standard-properties"></a>Propiedades estándar  
 Cada miembro tiene un conjunto de propiedades predeterminadas. En la tabla siguiente se enumeran estas propiedades predeterminadas.  
  
|Identificador de la propiedad|Significado|  
|-------------------------|-------------|  
|FORMAT_STRING|Un [!INCLUDE[msCoName](../includes/msconame-md.md)] cadena de formato de estilo de Office que la aplicación cliente puede utilizar para mostrar los valores de celda.|  
|VISIBLE|Valor que indica si el miembro calculado es visible en el conjunto de filas del esquema. Calculados visibles se pueden agregar miembros a un conjunto con el [AddCalculatedMembers](../mdx/addcalculatedmembers-mdx.md) función. Un valor distinto de cero indica que el miembro calculado es visible. El valor predeterminado de esta propiedad es *Visible*.<br /><br /> Los miembros calculados no visibles suelen utilizarse como pasos intermedios en miembros calculados más complejos. También otros tipos de miembro, como las medidas, pueden hacer referencia a estos miembros calculados.|  
|NON_EMPTY_BEHAVIOR|Medida o conjunto que utiliza MDX para determinar el comportamiento de los miembros calculados al resolver celdas vacías.|  
|CAPTION|Valor de cadena que especifica el título que usa la aplicación cliente para mostrar el miembro.|  
|DISPLAY_FOLDER|Valor de cadena que especifica la ruta de acceso a la carpeta donde la aplicación cliente mostrará el miembro. La aplicación cliente define el separador de niveles de carpetas. Para las herramientas y clientes proporcionados por [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], la barra diagonal inversa (\\) como separador de nivel. Si va a asignar varias carpetas para mostrar a un miembro definido, utilice un punto y coma (;) para separar las carpetas.|  
|ASSOCIATED_MEASURE_GROUP|Nombre del grupo de medida al que se asocia el miembro.|  
  
## <a name="see-also"></a>Vea también  
 [DROP MEMBER, instrucción &#40;MDX&#41;](../mdx/mdx-data-definition-drop-member.md)   
 [CREATE MEMBER, instrucción & #40; MDX & #41;](../mdx/mdx-data-definition-create-member.md)   
 [Instrucciones de definición de datos MDX &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
