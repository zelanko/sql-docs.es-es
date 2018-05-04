---
title: IMPORTACIÓN (DMX) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- IMPORT
dev_langs:
- DMX
helpviewer_keywords:
- IMPORT statement
- mining structures [DMX], importing
ms.assetid: c053bc88-2daf-4ebb-81d7-5a330250536d
caps.latest.revision: 42
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 162bc8fc7497d3e8b425e09b81c13a24adb75678
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="import-dmx"></a>IMPORT (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Carga un modelo o una estructura de minería de datos de un archivo de copia de seguridad de Analysis Services (.abf) en el servidor.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
IMPORT FROM <filename>  
```  
  
## <a name="arguments"></a>Argumentos  
 *nombre de archivo*  
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
 [Extensiones de minería de datos &#40;DMX&#41; las instrucciones de definición de datos](../dmx/dmx-statements-data-definition.md)   
 [Extensiones de minería de datos &#40;DMX&#41; instrucciones de manipulación de datos](../dmx/dmx-statements-data-manipulation.md)   
 [Extensiones de minería de datos &#40;DMX&#41; Referencia de instrucciones](../dmx/data-mining-extensions-dmx-statements.md)   
 [EXPORTAR &AMP;#40;DMX&AMP;#41;](../dmx/export-dmx.md)   
 [Exportar e importar objetos de minería de datos](../analysis-services/data-mining/export-and-import-data-mining-objects.md)  
  
  
