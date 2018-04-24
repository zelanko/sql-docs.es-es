---
title: Agregar registros mediante AddNew | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- AddNew method [ADO]
- ADO, adding data
- editing data [ADO], AddNew method
ms.assetid: cab4adff-f22f-4fb1-9217-f8138c795268
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 33a4570707bffdba987acf9976d9747188e82e9e
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2018
---
# <a name="adding-records-using-addnew-method"></a>Agregar registros mediante AddNew (método)
Ésta es la sintaxis básica de la **AddNew** método:

 *conjunto de registros*. AddNew *FieldList*, *valores*

 El *FieldList* y *valores* argumentos son opcionales. *FieldList* es un nombre único o una matriz de nombres o posiciones ordinales de los campos en el nuevo registro.

 El *valores* argumento es un valor único o una matriz de valores de los campos en el nuevo registro.

 Normalmente, cuando vaya a agregar un registro único, llamará a la **AddNew** método sin ningún argumento. En concreto, llamará **AddNew**; establezca la **valor** de cada campo en el nuevo registro; y, a continuación, llame a **actualización** o **UpdateBatch**, o ambos. Puede asegurarse de que su **Recordset** admite la adición de nuevos registros mediante el uso de la **admite** propiedad con el **adAddNew** constante enumerada.

 El código siguiente utiliza esta técnica para agregar un nuevo transportista al ejemplo **conjunto de registros**. SQL Server suministra el valor del campo ShipperID automáticamente. Por lo tanto, el código no intenta proporcionar un valor de campo para los nuevos registros.

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
 Dado que este código utiliza un desconectada **conjunto de registros** con un cursor de cliente en modo por lotes, debe volver a conectar el **Recordset** al origen de datos con un nuevo **conexión** objeto para poder invocar la **UpdateBatch** método para registrar los cambios en la base de datos. Esto se hace fácilmente mediante la nueva función **GetNewConnection**.
