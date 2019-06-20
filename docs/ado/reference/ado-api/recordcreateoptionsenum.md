---
title: RecordCreateOptionsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RecordCreateOptionsEnum
helpviewer_keywords:
- RecordCreateOptionsEnum enumeration [ADO]
ms.assetid: 6d746670-0850-4065-9cd4-168dea1d3ea9
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d57f1bc241e5e27618a9598895ea7be089ce20dd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66712012"
---
# <a name="recordcreateoptionsenum"></a>RecordCreateOptionsEnum
Especifica si una existente **registro** debe estar abierto o un nuevo **registro** creado para el [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto [abierto](../../../ado/reference/ado-api/open-method-ado-record.md) método. Los valores se pueden combinar con un operador AND.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adCreateCollection**|0x2000|Crea un nuevo **registro** en el nodo especificado por *origen* parámetro, en lugar de abrir uno existente **registro**. Si el origen apunta a un nodo existente, a continuación, se produce un error de tiempo de ejecución, a menos que **adCreateCollection** se combina con **adOpenIfExists** o **adCreateOverwrite**.|  
|**adCreateNonCollection**|0|Crea un nuevo **registro** typu [adSimpleRecord](../../../ado/reference/ado-api/recordtypeenum.md).|  
|**adCreateOverwrite**|0x4000000|Modifica las marcas de creación **adCreateCollection**, **adCreateNonCollection**, y **adCreateStructDoc**. Cuando o se usa con este valor y uno de los valores de indicador de creación, si la dirección URL de origen apunta a un nodo existente o **registro**, entonces el existente **registro** es sobrescritos y una en su lugar se crea uno nuevo. Este valor no se puede usar junto con **adOpenIfExists**.|  
|**adCreateStructDoc**|0x80000000|Crea un nuevo **registro** typu [adStructDoc](../../../ado/reference/ado-api/recordtypeenum.md), en lugar de abrir uno existente **registro**.|  
|**adFailIfNotExists**|-1|Predeterminado: Se produce un error en tiempo de ejecución si *origen* apunta a un nodo que no existe.|  
|**adOpenIfExists**|0x2000000|Modifica las marcas de creación **adCreateCollection**, **adCreateNonCollection**, y **adCreateStructDoc**. Cuando o se usa con este valor y uno de los valores de indicador de creación, si la dirección URL de origen apunta a un nodo existente o **registro** objeto, a continuación, debe abrir el proveedor existente **registro** en lugar de crear un nuevo uno. Este valor no se puede usar junto con **adCreateOverwrite**.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO y WFC  
 Estas constantes no tienen equivalentes de ADO y WFC.  
  
## <a name="applies-to"></a>Se aplica a  
 [Open (método) (registro de ADO)](../../../ado/reference/ado-api/open-method-ado-record.md)
