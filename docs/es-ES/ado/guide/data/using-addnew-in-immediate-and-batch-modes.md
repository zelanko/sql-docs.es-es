---
title: Usar AddNew de inmediato y modos de lote | Documentos de Microsoft
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
- ADO, editing data
- ADO, adding data
- editing data [ADO], AddNew method
ms.assetid: ed314bb9-e188-4658-a68c-a2abc49610be
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0e2c7f2cdd8a983572dc75a0a976e76289044f80
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="using-addnew-in-immediate-and-batch-modes"></a>Uso de AddNew de inmediato y modos de lote
El comportamiento de la **AddNew** método depende del modo de actualización de la **Recordset** objeto y si se pasan los *FieldList* y *valores*argumentos.  
  
 En modo de actualización inmediata (en el que el proveedor escribe los cambios en el origen de datos subyacente una vez que se llama a la **actualizar** método), la llamada a la **AddNew** método sin argumentos establece el  **EditMode** propiedad **adEditAdd.** El proveedor almacena en caché localmente los cambios de valor de campo. Llamar a la **actualización** método envía el nuevo registro a la base de datos y se restablece el **EditMode** propiedad **adEditNone.** Si se pasa el *FieldList* y *valores* argumentos, ADO envía inmediatamente el nuevo registro a la base de datos (no **actualización** es necesario llamar a); el **EditMode**  no cambia el valor de propiedad (**adEditNone**).  
  
 En modo de actualización por lotes, una llamada a la **AddNew** método sin argumentos establece la **EditMode** propiedad **adEditAdd**. El proveedor almacena en caché localmente los cambios de valor de campo. Llamar a la **actualización** método agrega el nuevo registro al actual **conjunto de registros** y restablece el **EditMode** propiedad **adEditNone**, pero el proveedor no envía los cambios a la base de datos subyacente hasta que llama a la **UpdateBatch** método. Si se pasa el *FieldList* y *valores* argumentos, ADO envía el nuevo registro en el proveedor de almacenamiento en una memoria caché; debe llamar a la **UpdateBatch** método para registrar el nuevo Registre la base de datos subyacente. Para obtener más información acerca de **actualización** y **UpdateBatch**, consulte [actualizar y conservar datos](../../../ado/guide/data/updating-and-persisting-data.md).
