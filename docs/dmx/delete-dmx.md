---
description: DELETE (DMX)
title: ELIMINAR (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c6050a387af893e984b95c036181b7f16a269dc0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491563"
---
# <a name="delete-dmx"></a>DELETE (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Borra un modelo de minería de datos, una estructura de minería datos, o una estructura de minería de datos y todos sus modelos de minería de datos asociados, según las cláusulas DMX (Extensiones de minería de datos) que utilice.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DELETE FROM [MINING MODEL] <model>[.CONTENT]  
DELETE FROM [MINING STRUCTURE] <structure>[.CONTENT]|[.CASES]  
```  
  
## <a name="arguments"></a>Argumentos  
 *model*  
 Identificador de modelo.  
  
 *structure*  
 Identificador de estructura.  
  
## <a name="remarks"></a>Observaciones  
 Si no especifica el **modelo** o la **estructura**de minería de datos, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] busca el tipo de objeto basándose en el nombre y procesa el objeto correcto. Si el servidor contiene una estructura y un modelo de minería de datos con el mismo nombre, se devuelve un error.  
  
 En la siguiente tabla se describen los resultados de usar las diferentes formas de sintaxis.  
  
|.|Resultado|  
|---------------|------------|  
|ELIMINAR DE LA ESTRUCTURA DE MINERÍA DE DATOS*\<structure>*<br /><br /> or<br /><br /> ELIMINAR de la estructura de minería de datos *\<structure>* . CONTENT|Realiza ProcessClear en la estructura de minería de datos. Se borra todo el contenido de la estructura de minería de datos y sus modelos de minería de datos asociados.|  
|ELIMINAR de la estructura de minería de datos *\<structure>* . VECES|Realiza ProcessClearStructureOnly en la estructura de minería de datos. Se borra todo el contenido de la estructura de minería de datos y se dejan intactos sus modelos de minería de datos asociados. La obtención de detalles de los modelos de minería de datos asociados produce un error tras el borrado de la estructura de minería de datos.|  
|ELIMINAR DEL MODELO DE MINERÍA DE DATOS*\<model>*<br /><br /> or<br /><br /> ELIMINAR del modelo de minería de datos *\<model>* . CONTENT|Realiza ProcessClear en el modelo de minería de datos, pero deja intactos los valores de estado. Los valores de estado son los estados posibles de una columna. Por ejemplo, los valores de estado de una columna de género serían masculino y femenino.|  
  
 Para obtener más información sobre los tipos de procesamiento, vea [elemento Type &#40;XMLA&#41;](https://docs.microsoft.com/analysis-services/xmla/xml-elements-properties/type-element-xmla).  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se quita todo el contenido del modelo NB_Sample.  
  
```  
DELETE FROM NB_Sample.CONTENT  
```  
  
## <a name="see-also"></a>Consulte también  
 [Extensiones de minería de datos &#40;DMX&#41; instrucciones de definición de datos](../dmx/dmx-statements-data-definition.md)   
 [Extensiones de minería de datos &#40;DMX&#41; instrucciones de manipulación de datos](../dmx/dmx-statements-data-manipulation.md)   
 [Referencia de instrucciones de Extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
