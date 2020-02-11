---
title: UPDATE MEMBER (instrucción, MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 73a2bf2973d8c4f8f9bf9ac886728fb45250343f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68038139"
---
# <a name="mdx-data-definition---update-member"></a>Definición de datos de MDX: UPDATE MEMBER


  Actualiza un miembro calculado existente.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
UPDATE MEMBER Cube_Name.Member_Name   
   AS MDX_Expression  
      [,Property_Name = Property_Value, ...n]  
......[,SCOPE_ISOLATION = CUBE]  
```  
  
## <a name="arguments"></a>Argumentos  
 *Cube_Name*  
 Expresión de cadena válida que especifica el nombre del cubo que contiene el miembro.  
  
 *Member_Name*  
 Expresión de cadena válida que especifica el nombre de un miembro existente.  
  
 *MDX_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida a la que se va a actualizar el miembro.  
  
 *Property_Name*  
 Cadena válida que especifica el nombre de una propiedad de miembro calculado.  
  
 *Property_Value*  
 Expresión escalar válida que especifica el valor de la propiedad para el miembro calculado.  
  
## <a name="remarks"></a>Observaciones  
 La instrucción UPDATE MEMBER actualiza un miembro calculado existente conservando la prioridad relativa de este miembro con respecto a otros cálculos. Por consiguiente, no puede utilizar la instrucción UPDATE MEMBER para cambiar SOLVEORDER.  
  
 Una instrucción UPDATE MEMBER no se puede especificar en el script MDX para un cubo.  
  
 Si especifica un cubo distinto del que está conectado actualmente, se genera un error. Por lo tanto, debe utilizar CURRENTCUBE en lugar de un nombre de cubo para indicar el cubo actual.  
  
 Para obtener más información acerca de las propiedades de miembro definidas por OLE DB, vea la documentación de OLE DB.  
  
## <a name="standard-properties"></a>Propiedades estándar  
 Cada miembro tiene un conjunto de propiedades predeterminadas. En la tabla siguiente se enumeran estas propiedades predeterminadas.  
  
|Identificador de la propiedad|Significado|  
|-------------------------|-------------|  
|FORMAT_STRING|Cadena de formato de estilo de Office que la aplicación cliente puede usar para mostrar valores de celda.|  
|VISIBLE|Valor que indica si el miembro calculado es visible en el conjunto de filas del esquema. Los miembros calculados visibles se pueden agregar a un conjunto con la función [AddCalculatedMembers](../mdx/addcalculatedmembers-mdx.md) . Un valor distinto de cero indica que el miembro calculado es visible. El valor predeterminado de esta propiedad es *visible*.<br /><br /> Los miembros calculados no visibles suelen utilizarse como pasos intermedios en miembros calculados más complejos. También otros tipos de miembro, como las medidas, pueden hacer referencia a estos miembros calculados.|  
|NON_EMPTY_BEHAVIOR|Medida o conjunto que utiliza MDX para determinar el comportamiento de los miembros calculados al resolver celdas vacías.|  
|CAPTION|Valor de cadena que especifica el título que usa la aplicación cliente para mostrar el miembro.|  
|DISPLAY_FOLDER|Valor de cadena que especifica la ruta de acceso a la carpeta donde la aplicación cliente mostrará el miembro. La aplicación cliente define el separador de niveles de carpetas. Para las herramientas y clientes proporcionados [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]por, la barra diagonal\\inversa () como separador de nivel. Si va a asignar varias carpetas para mostrar a un miembro definido, utilice un punto y coma (;) para separar las carpetas.|  
|ASSOCIATED_MEASURE_GROUP|Nombre del grupo de medida al que se asocia el miembro.|  
  
## <a name="see-also"></a>Consulte también  
 [Instrucción DROP MEMBER &#40;MDX&#41;](../mdx/mdx-data-definition-drop-member.md)   
 [Instrucción CREATE MEMBER &#40;MDX&#41;](../mdx/mdx-data-definition-create-member.md)   
 [Instrucciones de definición de datos de MDX &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
