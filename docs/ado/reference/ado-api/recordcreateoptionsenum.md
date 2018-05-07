---
title: RecordCreateOptionsEnum | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RecordCreateOptionsEnum
helpviewer_keywords:
- RecordCreateOptionsEnum enumeration [ADO]
ms.assetid: 6d746670-0850-4065-9cd4-168dea1d3ea9
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3109e7e7116fac22e007c65167bb718edf2b29b7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="recordcreateoptionsenum"></a>RecordCreateOptionsEnum
Especifica si una existente **registro** debe estar abierto o un nuevo **registro** creado para la [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto [abiertos](../../../ado/reference/ado-api/open-method-ado-record.md) método. Los valores se pueden combinar con un operador AND.  
  
|Constante|Value|Description|  
|--------------|-----------|-----------------|  
|**adCreateCollection**|0x2000|Crea un nuevo **registro** en el nodo especificado por *origen* parámetro, en lugar de abrir uno existente **registro**. Si el origen apunta a un nodo existente, a continuación, se produce un error en tiempo de ejecución, a menos que **adCreateCollection** se combina con **adOpenIfExists** o **adCreateOverwrite**.|  
|**adCreateNonCollection**|0|Crea un nuevo **registro** de tipo [adSimpleRecord](../../../ado/reference/ado-api/recordtypeenum.md).|  
|**adCreateOverwrite**|0x4000000|Modifica los indicadores de creación **adCreateCollection**, **adCreateNonCollection**, y **adCreateStructDoc**. Cuando se utiliza con este valor y uno de los valores de indicador de creación, si la dirección URL de origen apunta a un nodo existente o **registro**, a continuación, existente **registro** es sobrescribe y una nueva se crea en su lugar uno. Este valor no se puede usar junto con **adOpenIfExists**.|  
|**adCreateStructDoc**|0x80000000|Crea un nuevo **registro** de tipo [adStructDoc](../../../ado/reference/ado-api/recordtypeenum.md), en lugar de abrir uno existente **registro**.|  
|**adFailIfNotExists**|-1|Predeterminado: Se produce un error en tiempo de ejecución si *origen* apunta a un nodo inexistente.|  
|**adOpenIfExists**|0x2000000|Modifica los indicadores de creación **adCreateCollection**, **adCreateNonCollection**, y **adCreateStructDoc**. Cuando se utiliza con este valor y uno de los valores de indicador de creación, si la dirección URL de origen apunta a un nodo existente o **registro** objeto, a continuación, debe abrir el proveedor existente **registro** en lugar de crear un nuevo uno. Este valor no se puede usar junto con **adCreateOverwrite**.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Estas constantes no tienen equivalentes ADO/WFC.  
  
## <a name="applies-to"></a>Se aplica a  
 [Open (método) (registro de ADO)](../../../ado/reference/ado-api/open-method-ado-record.md)
