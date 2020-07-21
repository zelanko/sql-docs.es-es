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
author: rothja
ms.author: jroth
ms.openlocfilehash: c3dbcdf4ab089968741a4d0b08b7b02d1324f26d
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761401"
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
