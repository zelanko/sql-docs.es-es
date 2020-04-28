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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 807a8d7e5757a2caf76f100a1ae51c4a8a3f4e98
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67931143"
---
# <a name="saveoptionsenum"></a>SaveOptionsEnum
Especifica si se debe crear o sobrescribir un archivo al guardar desde un objeto de [flujo](../../../ado/reference/ado-api/stream-object-ado.md) . Los valores pueden ser **adSaveCreateNotExist** o **adSaveCreateOverWrite**.  
  
|Constante|Value|Descripción|  
|--------------|-----------|-----------------|  
|**adSaveCreateNotExist**|1|Predeterminada. Crea un nuevo archivo si el archivo especificado por el parámetro *filename* todavía no existe.|  
|**adSaveCreateOverWrite**|2|Sobrescribe el archivo con los datos del objeto de **secuencia** abierto actualmente, si el archivo especificado por el parámetro *filename* ya existe. Si el archivo especificado por el parámetro *filename* no existe, se crea un archivo nuevo.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO/WFC  
 Estas constantes no tienen equivalentes de ADO/WFC.  
  
## <a name="applies-to"></a>Se aplica a  
 [Método SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)
