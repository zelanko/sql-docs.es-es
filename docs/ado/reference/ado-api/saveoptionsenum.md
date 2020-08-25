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
ms.openlocfilehash: edac11f61b003307703ec13daed8022b8af31bae
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777564"
---
# <a name="saveoptionsenum"></a>SaveOptionsEnum
Especifica si se debe crear o sobrescribir un archivo al guardar desde un objeto de [flujo](./stream-object-ado.md) . Los valores pueden ser **adSaveCreateNotExist** o **adSaveCreateOverWrite**.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adSaveCreateNotExist**|1|Predeterminada. Crea un nuevo archivo si el archivo especificado por el parámetro *filename* todavía no existe.|  
|**adSaveCreateOverWrite**|2|Sobrescribe el archivo con los datos del objeto de **secuencia** abierto actualmente, si el archivo especificado por el parámetro *filename* ya existe. Si el archivo especificado por el parámetro *filename* no existe, se crea un archivo nuevo.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO/WFC  
 Estas constantes no tienen equivalentes de ADO/WFC.  
  
## <a name="applies-to"></a>Se aplica a  
 [Método SaveToFile](./savetofile-method.md)