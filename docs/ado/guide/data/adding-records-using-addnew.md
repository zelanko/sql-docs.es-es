---
title: Agregar registros mediante AddNew | Microsoft Docs
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
- editing data [ADO], AddNew method
ms.assetid: cab4adff-f22f-4fb1-9217-f8138c795268
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 36f6bad9a8f0d74a81d02ce64c78d7a91ddc0fa8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67926284"
---
# <a name="adding-records-using-addnew-method"></a>Agregar registros mediante el método AddNew
Esta es la sintaxis básica del método **AddNew** :

 *conjunto de registros*. AgregarNuevo *FieldList*, *valores*

 Los argumentos *FieldList* y *Values* son opcionales. *FieldList* es un nombre único o una matriz de nombres o posiciones ordinales de los campos del nuevo registro.

 El argumento *valores* es un valor único o una matriz de valores para los campos del nuevo registro.

 Normalmente, cuando se intenta agregar un solo registro, se llama al método **AddNew** sin ningún argumento. En concreto, llamará a **AddNew**; Establezca el **valor** de cada campo en el nuevo registro. a continuación, llame a **Update** o a **UpdateBatch**, o a ambos. Puede asegurarse de que el **conjunto de registros** admite la adición de nuevos registros mediante la propiedad **Supports** con la constante enumerada **adAddNew** .

 El código siguiente usa esta técnica para agregar un nuevo remitente al **conjunto de registros**de ejemplo. SQL Server proporciona automáticamente el valor del campo ShipperID. Por lo tanto, el código no intenta proporcionar un valor de campo para los nuevos registros.

```
'BeginAddNew1.1
If objRs.Supports(adAddNew) Then
    With objRs
        .AddNew
        .Fields("CompanyName") = "Sample Shipper"
        .Fields("Phone") = "(931) 555-6334"
        .Update
    End With
End If
'EndAddNew1.1
```

## <a name="remarks"></a>Observaciones
 Dado que este código usa un conjunto de **registros** desconectado con un cursor del lado cliente en modo por lotes, debe volver a conectar el **conjunto de registros** al origen de datos con un nuevo objeto de **conexión** antes de poder llamar al método **UpdateBatch** para publicar los cambios en la base de datos. Esto se realiza fácilmente mediante el uso de la nueva función **GetNewConnection**.
