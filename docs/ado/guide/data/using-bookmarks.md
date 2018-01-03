---
title: Utilizar marcadores | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- bookmarks [ADO]
- Recordset object [ADO]
ms.assetid: cca244e6-84f8-4394-bca9-f7a819b8f4df
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7cbabea62b99f36adb2adf9f12e52d80644f33ea
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="using-bookmarks"></a>Utilizar marcadores
A menudo resulta útil volver directamente a un registro específico después de haberse movido por el **Recordset** sin tener que desplazarse a través de cada registro y comparar valores. Por ejemplo, si se intenta buscar un registro mediante el **buscar** método, pero la búsqueda no devuelve ningún registro, se colocan automáticamente en cualquier extremo de la **conjunto de registros**. Si el proveedor es compatible con ellos, se pueden utilizar marcadores para marcar su lugar antes de usar el **buscar** método para que pueda volver a su ubicación. Un marcador es un **Variant** escriba el valor que identifica de forma única un registro en un **Recordset** objeto.  
  
 También puede utilizar una matriz variant de marcadores con el **filtro de conjunto de registros** método para filtrar según un conjunto de registros seleccionados. Para obtener más información acerca de esta técnica, vea Filtrar los resultados en el tema [trabajar con conjuntos de registros](../../../ado/guide/data/working-with-recordsets.md), más adelante en esta sección.  
  
 Puede usar el **marcador** propiedad para obtener un marcador para un registro, o establecer el registro actual un **Recordset** objeto en el registro identificado por un marcador válido. El siguiente código utiliza el **marcador** propiedad para establecer un marcador y, a continuación, volver al registro del marcador después de moverse a otro registro. Para determinar si su **Recordset** admite marcadores, use el **admite** método.  
  
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
  
 Excepto en el caso de clonado **conjuntos de registros**, los marcadores son únicos para la **Recordset** en que se crearon, incluso si se utiliza el mismo comando. Esto significa que no se puede utilizar un **marcador** obtenido de una **Recordset** para mover con el mismo registro en un segundo **Recordset** abierto con el mismo comando.
