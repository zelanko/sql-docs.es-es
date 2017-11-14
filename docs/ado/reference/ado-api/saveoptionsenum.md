---
title: SaveOptionsEnum | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- SaveOptionsEnum
helpviewer_keywords:
- SaveOptionsEnum enumeration [ADO]
ms.assetid: 59339100-6e29-48d1-aea3-6873796d186b
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 97f3d76d9fed33de5ba79d84a062891316c70ae0
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="saveoptionsenum"></a>SaveOptionsEnum
Especifica si se debe crear un archivo o sobrescribir al guardar desde un [flujo](../../../ado/reference/ado-api/stream-object-ado.md) objeto. Los valores pueden ser **adSaveCreateNotExist** o **adSaveCreateOverWrite**...  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adSaveCreateNotExist**|1|Predeterminado: Crea un nuevo archivo si el archivo especificado por el *FileName* parámetro aún no existe.|  
|**adSaveCreateOverWrite**|2|Sobrescribe el archivo con los datos de abiertos actualmente **flujo** objeto, si el archivo especificado por el *Filename* parámetro ya existe. Si el archivo especificado por el *nombre de archivo* no existe el parámetro, se crea un nuevo archivo.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Estas constantes no tienen equivalentes ADO/WFC.  
  
## <a name="applies-to"></a>Se aplica a  
 [Método SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)

