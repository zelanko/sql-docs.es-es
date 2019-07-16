---
title: EXPORTACIÓN (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2cf3cf85b0efb024d65744f6eea0f5eea47ead83
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68074852"
---
# <a name="export-dmx"></a>EXPORT (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Extrae un objeto de modelo o de estructura de minería de datos del servidor a un archivo de copia de seguridad de Analysis Services (.abf).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
EXPORT <object type> <object name>[, <object name>] [<object type> <object name>[, <object name] ] TO <filename> [WITH DEPENDENCIES]  
```  
  
## <a name="arguments"></a>Argumentos  
 *tipo de objeto*  
 Tipo opcional de objeto que se va a exportar (modelo de minería de datos o estructura de minería de datos).  
  
 *nombre de objeto*  
 Opcional. Nombre del objeto que se va a exportar.  
  
 *filename*  
 Nombre y ubicación del archivo que se va a exportar como cadena.  
  
## <a name="remarks"></a>Comentarios  
 Si la instrucción especifica un modelo de minería de datos, el archivo resultante contendrá también una estructura de minería de datos asociada. Si la instrucción especifica **WITH DEPENDENCIES**, todos los objetos necesarios para procesar el objeto (por ejemplo, el origen de datos y la vista del origen de datos) se incluyen en el archivo abf.  
  
 Debe ser una base de datos o el administrador del servidor para exportar o importar objetos desde una [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] base de datos.  
  
## <a name="export-mining-structure-example"></a>Ejemplo de exportación de estructura de minería de datos  
 En el siguiente ejemplo se exportan las estructuras de minería de datos Targeted Mailing y Forecasting, y el modelo de minería de datos Association a una ubicación de archivos específica. Puesto que el modelo Association forma parte de la estructura de minería de datos Market Basket, también se exporta la estructura Market Basket. Otros modelos de minería de datos que puedan existir como parte de la estructura de minería de datos Market Basket no se exportarán porque el modelo Association se exportó con **modelo de minería de datos**, no **estructura de minería de datos**.  
  
```  
EXPORT MINING STRUCTURE [Targeted Mailing], [Forecasting] MINING MODEL Association TO 'C:\TM_NEW.abf'  
```  
  
## <a name="export-mining-model-example"></a>Ejemplo de exportación de modelo de minería de datos  
 En el siguiente ejemplo se exporta el modelo de minería de datos Association a una ubicación de archivos especificada. Puesto que la instrucción especifica **WITH DEPENDENCIES**, el origen de datos y objetos de vista del origen de datos también se incluyen en el archivo abf.  
  
```  
EXPORT MINING MODEL [Association] TO 'C:\Association_NEW.abf' WITH DEPENDENCIES  
```  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de minería de datos &#40;DMX&#41; instrucciones de definición de datos](../dmx/dmx-statements-data-definition.md)   
 [Extensiones de minería de datos &#40;DMX&#41; instrucciones de manipulación de datos](../dmx/dmx-statements-data-manipulation.md)   
 [Extensiones de minería de datos &#40;DMX&#41; referencia de instrucciones](../dmx/data-mining-extensions-dmx-statements.md)   
 [IMPORTACIÓN &#40;DMX&#41;](../dmx/import-dmx.md)   
 [Exportar e importar objetos de minería de datos](../analysis-services/data-mining/export-and-import-data-mining-objects.md)  
  
  
