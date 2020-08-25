---
description: Agregar registros a un conjunto de registros
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
ms.openlocfilehash: e38dbfbf8b0a92a0d1a8a2eff1b8b8d4d5374057
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806706"
---
# <a name="adding-records-to-a-recordset"></a>Agregar registros a un conjunto de registros
Use el método **AddNew** para crear e inicializar un nuevo registro en un **conjunto de registros**existente. Puede usar el método **Supports** con un valor **CursorOptionEnum** de **adAddNew** para comprobar si puede agregar registros al objeto de **conjunto de registros** actual.

 Después de llamar al método **AddNew** , el nuevo registro se convierte en el registro actual y permanece actual después de llamar al método **Update** . Si el objeto de **conjunto de registros** no admite marcadores, es posible que no pueda obtener acceso al nuevo registro una vez que se haya movido a otro registro. Por lo tanto, dependiendo del tipo de cursor, puede que tenga que llamar al método **Requery** para que el nuevo registro sea accesible.

 Si llama a **AddNew** mientras edita el registro actual o al agregar un nuevo registro, ADO llama al método **Update** para guardar los cambios y, a continuación, crea el nuevo registro.

 Esta sección contiene los temas siguientes.

-   [Agregar registros mediante AddNew](./adding-records-using-addnew.md)

-   [Agregar varios campos y valores](./adding-multiple-fields.md)

-   [Determinar el modo de edición](./determining-edit-mode.md)

-   [Uso de AddNew de inmediato y modos de lote](./using-addnew-in-immediate-and-batch-modes.md)