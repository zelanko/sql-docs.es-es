---
title: RecordOpenOptionsEnum | Documentos de Microsoft
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- RecordOpenOptionsEnum
helpviewer_keywords:
- RecordOpenOptionsEnum enumeration [ADO]
ms.assetid: 9028aba4-90fc-4dfc-88e4-fa8a7b6fedee
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 157b0683dc9d68e4fb00dce0d4a468fa5f622179
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="recordopenoptionsenum"></a>RecordOpenOptionsEnum
Especifica opciones para abrir un [registro](../../../ado/reference/ado-api/record-object-ado.md). Estos valores pueden combinarse mediante o.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adDelayFetchFields**|0x8000|Indica al proveedor que los campos asociados a la **registro** no es necesario que se recuperen inicialmente, pero se puede recuperar en el primer intento de obtener acceso al campo. El comportamiento predeterminado, indicado por la ausencia de este indicador, consiste en recuperar todos los **registro** campos de objeto.|  
|**adDelayFetchStream**|0x4000|Indica al proveedor que la secuencia predeterminada asociada con el **registro** no es necesario que se recuperen inicialmente. El comportamiento predeterminado, indicado por la ausencia de este indicador, consiste en recuperar la secuencia predeterminada asociada con el **registro** objeto.|  
|**adOpenAsync**|0x1000|Indica que la **registro** objeto se abre en modo asincrónico.|  
|**adOpenExecuteCommand**|0x10000|Indica que la cadena de origen contiene el texto del comando que se debe ejecutar. Este valor es equivalente a la **adCmdText** opción **Recordset.Open**.|  
|**adOpenRecordUnspecified**|-1|Predeterminado: Indica que no se especifican opciones.|  
|**adOpenOutput**|0x800000|Que indica si el origen apunta a un nodo que contiene una secuencia de comandos ejecutable (como un. Página ASP), a continuación, abrir **registro** contendrá los resultados de la secuencia de comandos ejecutada. Este valor sólo es válido con registros de no colección.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Estas constantes no tienen equivalentes ADO/WFC.  
  
## <a name="applies-to"></a>Se aplica a  
 [Open (método) (registro de ADO)](../../../ado/reference/ado-api/open-method-ado-record.md)
