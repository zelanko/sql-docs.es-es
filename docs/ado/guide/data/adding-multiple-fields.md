---
description: Agregar varios campos y valores
title: Agregar varios campos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- AddNew method [ADO]
- ADO, adding data
- editing data [ADO], adding multiple fields
- editing data [ADO], AddNew method
ms.assetid: f3648ef4-9f36-4991-a868-83a617389844
author: rothja
ms.author: jroth
ms.openlocfilehash: e2543741749c1521526aea18bc4600168559eb45
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453897"
---
# <a name="adding-multiple-fields-and-values"></a>Agregar varios campos y valores
En ocasiones, puede ser más eficaz pasar en una matriz de campos y sus valores correspondientes al método **AddNew** , en lugar de establecer el **valor** varias veces para cada nuevo campo. Si *FieldList* es una matriz, *los valores* también deben ser una matriz con el mismo número de miembros; de lo contrario, se produce un error. El orden de los nombres de campo debe coincidir con el orden de los valores de campo de cada matriz. En el código siguiente se pasa una matriz de campos y una matriz de valores al método **AddNew** .

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
