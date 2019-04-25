---
title: IMPORT (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4987701deb466148253c8418c88683d2dbfbc16b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62506067"
---
# <a name="import-dmx"></a>IMPORT (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Carga un modelo o una estructura de minería de datos de un archivo de copia de seguridad de Analysis Services (.abf) en el servidor.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
IMPORT FROM <filename>  
```  
  
## <a name="arguments"></a>Argumentos  
 *filename*  
 Cadena que contiene el nombre y la ubicación del archivo que se va a importar.  
  
## <a name="remarks"></a>Comentarios  
 Si no se especifica ningún objeto, se carga todo el contenido del archivo .dmb. Si el archivo .dmb incluye una base de datos que no existe en el servidor, se creará la base de datos.  
  
 Debe ser administrador de base de datos o de servidor para exportar o importar objetos.  
  
## <a name="import-from-file-example"></a>Ejemplo de importación desde archivo  
 En el ejemplo siguiente se importa el contenido completo del archivo que contiene la estructura y el modelo de asociación en el servidor actual.  
  
```  
IMPORT FROM 'C:\TEMP\Association_NEW.dmb'  
```  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de minería de datos &#40;DMX&#41; instrucciones de definición de datos](../dmx/dmx-statements-data-definition.md)   
 [Extensiones de minería de datos &#40;DMX&#41; instrucciones de manipulación de datos](../dmx/dmx-statements-data-manipulation.md)   
 [Extensiones de minería de datos &#40;DMX&#41; referencia de instrucciones](../dmx/data-mining-extensions-dmx-statements.md)   
 [EXPORT &#40;DMX&#41;](../dmx/export-dmx.md)   
 [Exportar e importar objetos de minería de datos](../analysis-services/data-mining/export-and-import-data-mining-objects.md)  
  
  
