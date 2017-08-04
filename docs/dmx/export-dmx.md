---
title: "EXPORTACIÓN (DMX) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- EXPORT
dev_langs:
- DMX
helpviewer_keywords:
- exporting mining models
- exporting mining structures
- mining structures [DMX], exporting
- EXPORT statement
ms.assetid: 97617071-e560-4080-81af-a80276fc0823
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: bfc3e8344d1c6967185979c0970be6d49b572500
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="export-dmx"></a>EXPORT (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Extrae un objeto de modelo o de estructura de minería de datos del servidor a un archivo de copia de seguridad de Analysis Services (.abf).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
EXPORT <object type> <object name>[, <object name>] [<object type> <object name>[, <object name] ] TO <filename> [WITH DEPENDENCIES]  
```  
  
## <a name="arguments"></a>Argumentos  
 *tipo de objeto*  
 Opcional el tipo de objeto que se va a exportar (modelo de minería de datos o la estructura de minería de datos).  
  
 *nombre de objeto*  
 Opcional. Nombre del objeto que se va a exportar.  
  
 *nombre de archivo*  
 Nombre y ubicación del archivo que se va a exportar como cadena.  
  
## <a name="remarks"></a>Comentarios  
 Si la instrucción especifica un modelo de minería de datos, el archivo resultante contendrá también una estructura de minería de datos asociada. Si la instrucción especifica **WITH DEPENDENCIES**, todos los objetos necesarios para procesar el objeto (por ejemplo, el origen de datos y la vista del origen de datos) se incluyen en el archivo abf.  
  
 Debe ser una base de datos o el administrador del servidor para exportar o importar objetos desde una [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] base de datos.  
  
## <a name="export-mining-structure-example"></a>Ejemplo de exportación de estructura de minería de datos  
 En el siguiente ejemplo se exportan las estructuras de minería de datos Targeted Mailing y Forecasting, y el modelo de minería de datos Association a una ubicación de archivos específica. Puesto que el modelo Association forma parte de la estructura de minería de datos Market Basket, también se exporta la estructura Market Basket. Otros modelos de minería de datos que existan como parte de la estructura de minería de datos de la cesta no se exportarán porque el modelo de asociación se exportó utilizando **modelo de minería de datos**, no **estructura de minería de datos**.  
  
```  
EXPORT MINING STRUCTURE [Targeted Mailing], [Forecasting] MINING MODEL Association TO 'C:\TM_NEW.abf'  
```  
  
## <a name="export-mining-model-example"></a>Ejemplo de exportación de modelo de minería de datos  
 En el siguiente ejemplo se exporta el modelo de minería de datos Association a una ubicación de archivos especificada. Dado que la instrucción especifica **WITH DEPENDENCIES**, el origen de datos y objetos de vista de origen de datos también se incluyen en el archivo abf.  
  
```  
EXPORT MINING MODEL [Association] TO 'C:\Association_NEW.abf' WITH DEPENDENCIES  
```  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de minería de datos &#40; DMX &#41; Instrucciones de definición de datos](../dmx/dmx-statements-data-definition.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Instrucciones de manipulación de datos](../dmx/dmx-statements-data-manipulation.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Referencia de instrucciones](../dmx/data-mining-extensions-dmx-statements.md)   
 [IMPORTAR &#40; DMX &#41;](../dmx/import-dmx.md)   
 [Exportar e importar objetos de minería de datos](../analysis-services/data-mining/export-and-import-data-mining-objects.md)  
  
  

