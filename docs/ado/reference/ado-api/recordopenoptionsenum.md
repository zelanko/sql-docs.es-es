---
title: RecordOpenOptionsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RecordOpenOptionsEnum
helpviewer_keywords:
- RecordOpenOptionsEnum enumeration [ADO]
ms.assetid: 9028aba4-90fc-4dfc-88e4-fa8a7b6fedee
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c0ed637d8e77ef7fc152f994da81db010fa80900
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66712153"
---
# <a name="recordopenoptionsenum"></a>RecordOpenOptionsEnum
Especifica opciones para abrir un [registro](../../../ado/reference/ado-api/record-object-ado.md). Estos valores se pueden combinar mediante el uso de o.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adDelayFetchFields**|0x8000|Indica al proveedor que los campos asociados con el **registro** no es necesario que se recuperen inicialmente, pero se pueden recuperar en el primer intento de obtener acceso al campo. El comportamiento predeterminado, indicado por la ausencia de este indicador, consiste en recuperar todos los **registro** campos de objeto.|  
|**adDelayFetchStream**|0x4000|Indica al proveedor que la secuencia predeterminada asociada con el **registro** no es necesario que se recuperen inicialmente. El comportamiento predeterminado, indicado por la ausencia de este indicador, consiste en recuperar la secuencia predeterminada asociada con el **registro** objeto.|  
|**adOpenAsync**|0x1000|Indica que el **registro** objeto se abre en modo asincrónico.|  
|**adOpenExecuteCommand**|0x10000|Indica que la cadena de origen contiene el texto del comando que se debe ejecutar. Este valor es equivalente a la **adCmdText** opción **Recordset.Open**.|  
|**adOpenRecordUnspecified**|-1|Predeterminado: Indica que no se especifican opciones.|  
|**adOpenOutput**|0x800000|Que indica si el origen apunta a un nodo que contiene una secuencia de comandos ejecutable (como un. Página ASP), a continuación, abrir **registro** contendrá los resultados de la secuencia de comandos ejecutada. Este valor solo es válido con los registros que no sea de colección.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO y WFC  
 Estas constantes no tienen equivalentes de ADO y WFC.  
  
## <a name="applies-to"></a>Se aplica a  
 [Open (método) (registro de ADO)](../../../ado/reference/ado-api/open-method-ado-record.md)
