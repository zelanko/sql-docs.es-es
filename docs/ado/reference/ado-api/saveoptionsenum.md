---
title: SaveOptionsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- SaveOptionsEnum
helpviewer_keywords:
- SaveOptionsEnum enumeration [ADO]
ms.assetid: 59339100-6e29-48d1-aea3-6873796d186b
author: rothja
ms.author: jroth
ms.openlocfilehash: 3423d215fa4a52286509769bb2ac0b75d2283a02
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82755837"
---
# <a name="saveoptionsenum"></a>SaveOptionsEnum
Especifica si se debe crear o sobrescribir un archivo al guardar desde un objeto de [flujo](../../../ado/reference/ado-api/stream-object-ado.md) . Los valores pueden ser **adSaveCreateNotExist** o **adSaveCreateOverWrite**.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adSaveCreateNotExist**|1|Predeterminada. Crea un nuevo archivo si el archivo especificado por el parámetro *filename* todavía no existe.|  
|**adSaveCreateOverWrite**|2|Sobrescribe el archivo con los datos del objeto de **secuencia** abierto actualmente, si el archivo especificado por el parámetro *filename* ya existe. Si el archivo especificado por el parámetro *filename* no existe, se crea un archivo nuevo.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO/WFC  
 Estas constantes no tienen equivalentes de ADO/WFC.  
  
## <a name="applies-to"></a>Se aplica a  
 [Método SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)
