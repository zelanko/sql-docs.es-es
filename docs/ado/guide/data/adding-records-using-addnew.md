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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926284"
---
# <a name="adding-records-using-addnew-method"></a>Agregar registros mediante AddNew (método)
Se trata de la sintaxis básica de la **AddNew** método:

 *conjunto de registros*. AddNew *FieldList*, *valores*

 El *FieldList* y *valores* argumentos son opcionales. *FieldList* es un nombre único o una matriz de nombres o las posiciones ordinales de los campos en el nuevo registro.

 El *valores* argumento es un valor único o una matriz de valores para los campos en el nuevo registro.

 Normalmente, cuando se desea agregar un registro único, llamará el **AddNew** método sin ningún argumento. En concreto, llamará **AddNew**; establezca la **valor** de cada campo en el nuevo registro; y, a continuación, llame a **actualización** o **UpdateBatch**, o ambos. Puede asegurarse de que su **Recordset** admite la adición de nuevos registros mediante el uso de la **admite** propiedad con el **adAddNew** constante enumerada.

 El código siguiente utiliza esta técnica para agregar un remitente nuevo al ejemplo **Recordset**. SQL Server suministra el valor del campo ShipperID automáticamente. Por lo tanto, el código no intenta proporcionar un valor de campo para los nuevos registros.

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

## <a name="remarks"></a>Comentarios
 Dado que este código usa un desconectado **Recordset** con un cursor de cliente en modo por lotes, debe volver a conectar el **Recordset** al origen de datos con un nuevo **conexión** objeto para poder invocar la **UpdateBatch** método para registrar los cambios en la base de datos. Esto se realiza fácilmente mediante el uso de la nueva función **GetNewConnection**.
