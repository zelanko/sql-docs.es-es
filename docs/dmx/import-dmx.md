---
title: "IMPORTACIÓN (DMX) | Documentos de Microsoft"
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
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 5510631430ed75a04dd9685d1197f60c64a85aa8
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="import-dmx"></a>IMPORT (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 [Extensiones de minería de datos &#40; DMX &#41; Instrucciones de definición de datos](../dmx/dmx-statements-data-definition.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Instrucciones de manipulación de datos](../dmx/dmx-statements-data-manipulation.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Referencia de instrucciones](../dmx/data-mining-extensions-dmx-statements.md)   
 [EXPORTAR &#40; DMX &#41;](../dmx/export-dmx.md)   
 [Exportar e importar objetos de minería de datos](../analysis-services/data-mining/export-and-import-data-mining-objects.md)  
  
  

