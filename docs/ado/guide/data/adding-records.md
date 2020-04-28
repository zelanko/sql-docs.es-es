---
title: Agregando registros | Microsoft Docs
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
- editing data [ADO], AddNew method
- editing data [ADO], adding data
ms.assetid: dd34669e-6f06-403b-9241-1c85c82aecc2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1f4ec0934fbf75de18f460abae84b8117e99f452
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67926264"
---
# <a name="adding-records-to-a-recordset"></a>Agregar registros a un conjunto de registros
Use el método **AddNew** para crear e inicializar un nuevo registro en un **conjunto de registros**existente. Puede usar el método **Supports** con un valor **CursorOptionEnum** de **adAddNew** para comprobar si puede agregar registros al objeto de **conjunto de registros** actual.

 Después de llamar al método **AddNew** , el nuevo registro se convierte en el registro actual y permanece actual después de llamar al método **Update** . Si el objeto de **conjunto de registros** no admite marcadores, es posible que no pueda obtener acceso al nuevo registro una vez que se haya movido a otro registro. Por lo tanto, dependiendo del tipo de cursor, puede que tenga que llamar al método **Requery** para que el nuevo registro sea accesible.

 Si llama a **AddNew** mientras edita el registro actual o al agregar un nuevo registro, ADO llama al método **Update** para guardar los cambios y, a continuación, crea el nuevo registro.

 Esta sección contiene los temas siguientes.

-   [Agregar registros mediante AddNew](../../../ado/guide/data/adding-records-using-addnew.md)

-   [Agregar varios campos y valores](../../../ado/guide/data/adding-multiple-fields.md)

-   [Determinar el modo de edición](../../../ado/guide/data/determining-edit-mode.md)

-   [Uso de AddNew de inmediato y modos de lote](../../../ado/guide/data/using-addnew-in-immediate-and-batch-modes.md)
