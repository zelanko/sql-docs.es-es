---
description: SaveOptionsEnum
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
ms.openlocfilehash: 27284d84bb89c0e742c5166589a60fdc949e7b2e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442197"
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
