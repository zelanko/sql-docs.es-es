---
title: Al agregar varios campos | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- AddNew method [ADO]
- ADO, adding data
- editing data [ADO], adding multiple fields
- editing data [ADO], AddNew method
ms.assetid: f3648ef4-9f36-4991-a868-83a617389844
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d9eac6c90c0605b157dcd83c1b23f34969f3f73c
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="adding-multiple-fields-and-values"></a>Agregar varios campos y valores
En ocasiones, puede que sea más eficaz para pasar una matriz de campos y sus valores correspondientes a la **AddNew** método, en lugar de configuración **valor** varias veces para cada nuevo campo. Si *FieldList* es una matriz, *valores* también debe ser una matriz con el mismo número de miembros; de lo contrario, se produce un error. El orden de los nombres de campo debe coincidir con el orden de los valores de campo en cada matriz. El código siguiente pasa una matriz de campos y una matriz de valores para la **AddNew** método.

```
'BeginAddNew2
    Dim avarFldNames As Variant
    Dim avarFldValues As Variant

    avarFldNames = Array("CompanyName", "Phone")
    avarFldValues = Array("Sample Shipper 2", "(931) 555-6334")

    If objRs1.Supports(adAddNew) Then
        objRs1.AddNew avarFldNames, avarFldValues
    End If

    'Re-establish a Connection and update
    Set objRs1.ActiveConnection = GetNewConnection
    objRs1.UpdateBatch
'EndAddNew2
```
