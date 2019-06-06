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
manager: jroth
ms.openlocfilehash: 537c5bfa6e1da125b562d4cc26820a2fcb5618fc
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66711377"
---
# <a name="saveoptionsenum"></a>SaveOptionsEnum
Especifica si se debe crear o sobrescribir al guardar desde un archivo de un [Stream](../../../ado/reference/ado-api/stream-object-ado.md) objeto. Los valores pueden ser **adSaveCreateNotExist** o **adSaveCreateOverWrite**...  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adSaveCreateNotExist**|1|Predeterminado: Crea un nuevo archivo si el archivo especificado por el *FileName* parámetro aún no existe.|  
|**adSaveCreateOverWrite**|2|Sobrescribe el archivo con los datos abiertos actualmente **Stream** objeto, si el archivo especificado por el *Filename* parámetro ya existe. Si el archivo especificado por el *Filename* parámetro no existe, se crea un nuevo archivo.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO y WFC  
 Estas constantes no tienen equivalentes de ADO y WFC.  
  
## <a name="applies-to"></a>Se aplica a  
 [Método SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)
