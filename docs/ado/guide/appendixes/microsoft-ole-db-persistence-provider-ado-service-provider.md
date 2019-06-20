---
title: Proveedor de persistencia OLE DB de Microsoft (proveedor de servicios de ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], OLE DB persistence provider
- persistence provider [ADO]
- OLE DB persistence provider [ADO]
ms.assetid: e75ef0dc-2016-4fcc-8918-23311c0d4e02
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d1ae4f8cba9235700edf410904862d39ed4f7f64
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66702996"
---
# <a name="microsoft-ole-db-persistence-provider-overview"></a>Introducción al proveedor de persistencia OLE DB de Microsoft
El proveedor de persistencia de Microsoft OLE DB permite guardar un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) de objetos en un archivo y restaurar más adelante que **Recordset** objeto desde el archivo. Información de esquema, datos y se conservan los cambios pendientes.

 Puede guardar el **Recordset** en el formato Advanced Data Table Gram (ADTG) propietario o el formato abierto de Extensible Markup Language (XML).

## <a name="provider-keyword"></a>Palabra clave del proveedor
 Para invocar este proveedor, especifique la siguiente palabra clave y valor en la cadena de conexión.

```vb
"Provider=MSPersist"
```

## <a name="errors"></a>Errores
 En la aplicación se pueden detectar los errores siguientes emitidos por este proveedor.

|Constante|Descripción|
|--------------|-----------------|
|E_BADSTREAM|El archivo abierto no tiene un formato válido (es decir, el formato no es ADTG o XML).|
|E_CANTPERSISTROWSET|El **Recordset** objeto guardado tiene características que le impiden que se almacena.|

## <a name="remarks"></a>Comentarios
 El proveedor de persistencia de Microsoft OLE DB no expone ninguna propiedad dinámica.

 Actualmente, solo parámetros jerárquicos **Recordset** objetos no se puede guardar.

 Para obtener más información acerca del almacenamiento persistente **Recordset** objetos, vea [persistencia de conjunto de registros](../../../ado/guide/data/more-about-recordset-persistence.md).

 Cuando se utiliza una secuencia para abrir un **Recordset,** no debería haber ningún parámetro especificado no sea el *origen* parámetro de la **abrir** método.

## <a name="see-also"></a>Vea también
[Proveedor de persistencia OLE DB de Microsoft (proveedor de servicios de ADO)](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)
