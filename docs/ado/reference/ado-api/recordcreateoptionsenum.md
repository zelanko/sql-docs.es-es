---
description: RecordCreateOptionsEnum
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 2fba315867e49935557d7bd6b3abe04c942e5a0a
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88772454"
---
# <a name="recordcreateoptionsenum"></a>RecordCreateOptionsEnum
Especifica si se debe abrir un **registro** existente o crear un nuevo **registro** para el método [Open](./open-method-ado-record.md) del objeto [Record](./record-object-ado.md) . Los valores se pueden combinar con un operador AND.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adCreateCollection**|0x2000|Crea un nuevo **registro** en el nodo especificado por el parámetro *source* , en lugar de abrir un **registro**existente. Si el origen apunta a un nodo existente, se produce un error en tiempo de ejecución, a menos que **adCreateCollection** se combine con **adOpenIfExists** o **adCreateOverwrite**.|  
|**adCreateNonCollection**|0|Crea un nuevo **registro** de tipo [adSimpleRecord](./recordtypeenum.md).|  
|**adCreateOverwrite**|0x4000000|Modifica las marcas de creación **adCreateCollection**, **adCreateNonCollection**y **adCreateStructDoc**. Cuando se usa o con este valor y uno de los valores de la marca de creación, si la dirección URL de origen apunta a un nodo o **registro**existente, se sobrescribe el **registro** existente y se crea uno nuevo en su lugar. Este valor no se puede usar junto con **adOpenIfExists**.|  
|**adCreateStructDoc**|0x80000000|Crea un nuevo **registro** de tipo [adStructDoc](./recordtypeenum.md), en lugar de abrir un **registro**existente.|  
|**adFailIfNotExists**|-1|Predeterminada. Da como resultado un error en tiempo de ejecución si el *origen* apunta a un nodo no existente.|  
|**adOpenIfExists**|0x2000000|Modifica las marcas de creación **adCreateCollection**, **adCreateNonCollection**y **adCreateStructDoc**. Cuando se usa o con este valor y uno de los valores de la marca de creación, si la dirección URL de origen apunta a un objeto de **registro** o nodo existente, el proveedor debe abrir el **registro** existente en lugar de crear uno nuevo. Este valor no se puede usar junto con **adCreateOverwrite**.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO/WFC  
 Estas constantes no tienen equivalentes de ADO/WFC.  
  
## <a name="applies-to"></a>Se aplica a  
 [Open (método) (registro de ADO)](./open-method-ado-record.md)