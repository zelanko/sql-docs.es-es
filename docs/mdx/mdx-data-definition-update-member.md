---
title: Instrucción UPDATE MEMBER (MDX) | Documentos de Microsoft
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: cd74ca9c5ebe5195dd65c88f657587583be55e92
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34579847"
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
  
## <a name="remarks"></a>Notas  
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
 [Instrucción CREATE MEMBER &#40;MDX&#41;](../mdx/mdx-data-definition-create-member.md)   
 [Instrucciones de definición de datos MDX &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
