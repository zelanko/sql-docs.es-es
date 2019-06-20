---
title: Uso de marcadores | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- bookmarks [ADO]
- Recordset object [ADO]
ms.assetid: cca244e6-84f8-4394-bca9-f7a819b8f4df
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c7e14e063d1aabcfce6391a85c0fcddbf0ff4e9f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66704617"
---
# <a name="using-bookmarks"></a>Utilizar marcadores
A menudo resulta útil volver directamente a un registro específico después de haberse movido por el **Recordset** sin tener que desplazarse por todos los registros y comparar valores. Por ejemplo, si se intenta buscar un registro mediante el **buscar** método, pero la búsqueda no devuelve ningún registro, se colocan automáticamente en los extremos de la **Recordset**. Si el proveedor es compatible con ellos, pueden utilizar marcadores para marcar la ubicación antes de usar el **buscar** método para que pueda volver a su ubicación. Un marcador es un **Variant** escriba el valor que identifica un registro en un **Recordset** objeto.  
  
 También puede usar una matriz variant de marcadores con el **filtro de conjunto de registros** método para filtrar según un conjunto de registros seleccionados. Para obtener más información sobre esta técnica, vea Filtrar los resultados en el tema [trabajar con conjuntos de registros](../../../ado/guide/data/working-with-recordsets.md), más adelante en esta sección.  
  
 Puede usar el **marcador** propiedad para obtener un marcador para un registro, o establecer el registro actual un **Recordset** objeto en el registro identificado por un marcador válido. El siguiente código utiliza el **marcador** propiedad para establecer un marcador y, a continuación, volver al registro del marcador después de moverse a otros registros. Para determinar si su **Recordset** admite marcadores, use el **admite** método.  
  
```  
'BeginBookmarkEg  
Dim varBookmark As Variant  
Dim blnCanBkmrk As Boolean  
  
objRs.Open strSQL, strConnStr, adOpenStatic, adLockOptimistic, adCmdText  
  
If objRs.RecordCount > 4 Then  
    objRs.Move 4                       ' move to the fifth record  
    blnCanBkmrk = objRs.Supports(adBookmark)  
    If blnCanBkmrk = True Then  
        varBookmark = objRs.Bookmark   ' record the bookmark  
        objRs.MoveLast                 ' move to a different record  
        objRs.Bookmark = varBookmark   ' return to the bookmarked (sixth) record  
    End If  
End If  
'EndBookmarkEg  
```  
  
 El [admite](../../../ado/reference/ado-api/supports-method.md) método se trata con más detalle más adelante.  
  
 Excepto en el caso de clonado **conjuntos de registros**, los marcadores son únicos para el **Recordset** en que fueron creadas, incluso si se utiliza el mismo comando. Esto significa que no se puede usar un **marcador** obtenida uno **Recordset** para mover en el mismo registro en un segundo **Recordset** abierto con el mismo comando.
