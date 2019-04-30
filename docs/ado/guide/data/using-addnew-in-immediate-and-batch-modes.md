---
title: Uso de AddNew de inmediato y modos de lote | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- AddNew method [ADO]
- ADO, editing data
- ADO, adding data
- editing data [ADO], AddNew method
ms.assetid: ed314bb9-e188-4658-a68c-a2abc49610be
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6295e4499a6f6f25f9111497012f2e9f1d6dc421
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63184936"
---
# <a name="using-addnew-in-immediate-and-batch-modes"></a>Uso de AddNew de inmediato y modos de lote
El comportamiento de la **AddNew** método depende del modo de actualización de la **Recordset** objeto y si se pasan los *FieldList* y *valores*argumentos.  
  
 En modo de actualización inmediata (en el que el proveedor escribe los cambios en el origen de datos subyacente cuando se llama el **actualizar** método), al llamar a la **AddNew** método sin argumentos establece el  **EditMode** propiedad **adEditAdd.** El proveedor almacena en caché localmente los cambios de valor de campo. Una llamada a la **actualización** método envía el nuevo registro a la base de datos y se restablece el **EditMode** propiedad **adEditNone.** Si se pasa el *FieldList* y *valores* argumentos, ADO envía inmediatamente el nuevo registro a la base de datos (no **actualización** es necesario llamar a); el **EditMode**  no cambia el valor de propiedad (**adEditNone**).  
  
 En modo de actualización por lotes, una llamada a la **AddNew** método sin argumentos establece el **EditMode** propiedad **adEditAdd**. El proveedor almacena en caché localmente los cambios de valor de campo. Una llamada a la **actualización** método agrega el nuevo registro a la actual **Recordset** y restablece el **EditMode** propiedad **adEditNone**, pero el proveedor no envía los cambios en la base de datos subyacente hasta que llame a la **UpdateBatch** método. Si se pasa el *FieldList* y *valores* argumentos, ADO envía el nuevo registro en el proveedor de almacenamiento en caché; debe llamar a la **UpdateBatch** método para registrar el nuevo Registre la base de datos subyacente. Para obtener más información acerca de **actualización** y **UpdateBatch**, consulte [actualizar y conservar datos](../../../ado/guide/data/updating-and-persisting-data.md).
