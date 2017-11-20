---
title: DELETE (DMX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DELETE
dev_langs:
- DMX
helpviewer_keywords:
- DELETE statement [DMX]
- mining structures [DMX], clearing
- clearing mining models
- deleting mining models
- mining models [Analysis Services], clearing
- deleting mining structures
ms.assetid: 5a8204c3-a3df-4d97-9c1d-d997d24c70e3
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 00be9b52e652e2a2456cdbcd589f048d8a971d47
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="delete-dmx"></a>DELETE (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Borra un modelo de minería de datos, una estructura de minería datos, o una estructura de minería de datos y todos sus modelos de minería de datos asociados, según las cláusulas DMX (Extensiones de minería de datos) que utilice.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DELETE FROM [MINING MODEL] <model>[.CONTENT]  
DELETE FROM [MINING STRUCTURE] <structure>[.CONTENT]|[.CASES]  
```  
  
## <a name="arguments"></a>Argumentos  
 *model*  
 Identificador de modelo.  
  
 *estructura*  
 Identificador de estructura.  
  
## <a name="remarks"></a>Comentarios  
 Si no se especifica **MINING MODEL** o **estructura de minería de datos**, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] busca el tipo de objeto basado en el nombre y procesa el objeto correcto. Si el servidor contiene una estructura y un modelo de minería de datos con el mismo nombre, se devuelve un error.  
  
 En la siguiente tabla se describen los resultados de usar las diferentes formas de sintaxis.  
  
|.|Resultado|  
|---------------|------------|  
|DELETE FROM MINING STRUCTURE*\<estructura >*<br /><br /> o bien<br /><br /> DELETE FROM MINING STRUCTURE*\<estructura >*. CONTENIDO|Realiza ProcessClear en la estructura de minería de datos. Se borra todo el contenido de la estructura de minería de datos y sus modelos de minería de datos asociados.|  
|DELETE FROM MINING STRUCTURE*\<estructura >*. CASOS|Realiza ProcessClearStructureOnly en la estructura de minería de datos. Se borra todo el contenido de la estructura de minería de datos y se dejan intactos sus modelos de minería de datos asociados. La obtención de detalles de los modelos de minería de datos asociados produce un error tras el borrado de la estructura de minería de datos.|  
|ELIMINAR del modelo de minería de datos*\<modelo >*<br /><br /> o bien<br /><br /> ELIMINAR del modelo de minería de datos*\<modelo >*. CONTENIDO|Realiza ProcessClear en el modelo de minería de datos, pero deja intactos los valores de estado. Los valores de estado son los estados posibles de una columna. Por ejemplo, los valores de estado de una columna de género serían masculino y femenino.|  
  
 Para obtener más información acerca de los tipos de procesamiento, vea [elemento Type &#40; XMLA &#41; ](../analysis-services/xmla/xml-elements-properties/type-element-xmla.md).  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se quita todo el contenido del modelo NB_Sample.  
  
```  
DELETE FROM NB_Sample.CONTENT  
```  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de minería de datos &#40; DMX &#41; Instrucciones de definición de datos](../dmx/dmx-statements-data-definition.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Instrucciones de manipulación de datos](../dmx/dmx-statements-data-manipulation.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Referencia de instrucciones](../dmx/data-mining-extensions-dmx-statements.md)  
  
  

