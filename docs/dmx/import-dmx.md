---
title: IMPORTAR (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2141a4f8ccc6e34ec3010ad3ce8e8e3789d09132
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892753"
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
 [Instrucciones de definición &#40;de&#41; datos DMX de extensiones de minería de datos](../dmx/dmx-statements-data-definition.md)   
 [Instrucciones de manipulación &#40;de&#41; datos DMX de extensiones de minería de datos](../dmx/dmx-statements-data-manipulation.md)   
 [Referencia de la &#40;instrucción&#41; DMX de extensiones de minería de datos](../dmx/data-mining-extensions-dmx-statements.md)   
 [EXPORTAR &#40;DMX&#41;](../dmx/export-dmx.md)   
 [Exportar e importar objetos de minería de datos](https://docs.microsoft.com/analysis-services/data-mining/export-and-import-data-mining-objects)  
  
  
