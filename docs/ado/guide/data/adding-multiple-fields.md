---
title: Al agregar varios campos | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fb62318b9f8eb03fbd3c9732dc8ad0caa9127d17
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63294426"
---
# <a name="adding-multiple-fields-and-values"></a>Agregar varios campos y valores
En ocasiones, podría ser más eficaz pasar una matriz de campos y sus valores correspondientes a la **AddNew** método, en lugar de la configuración **valor** varias veces para cada nuevo campo. Si *FieldList* es una matriz, *valores* también debe ser una matriz con el mismo número de miembros; de lo contrario, se produce un error. El orden de los nombres de campo debe coincidir con el orden de los valores de campo en cada matriz. El código siguiente pasa una matriz de campos y una matriz de valores para el **AddNew** método.

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
