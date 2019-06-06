---
title: Adición de registros | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 87d8358344d75cd6995d43d081abbec7aeaabe1c
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66701060"
---
# <a name="adding-records-to-a-recordset"></a>Agregar registros a un conjunto de registros
Use la **AddNew** método para crear e inicializar un nuevo registro en una existente **Recordset**. Puede usar el **admite** método con un **CursorOptionEnum** valor **adAddNew** para comprobar si puede agregar registros a la actual **delconjuntoderegistros** objeto.

 Después de llamar a la **AddNew** método, el nuevo registro se convierte en el registro actual y sigue siendo el actual después de llamar a la **actualización** método. Si el **Recordset** objeto no admite marcadores, es posible que no pueda acceder al registro de nuevo cuando se mueva a otro registro. Por lo tanto, dependiendo del tipo de cursor, es posible que deba llamar a la **Requery** método para que sea accesible el nuevo registro.

 Si se llama a **AddNew** mientras modifica el registro actual o agregar un nuevo registro, se llama ADO el **actualización** método para guardarlos cambios y, a continuación, crea el nuevo registro.

 Esta sección contiene los temas siguientes.

-   [Agregar registros mediante AddNew (método)](../../../ado/guide/data/adding-records-using-addnew.md)

-   [Agregar varios campos y valores](../../../ado/guide/data/adding-multiple-fields.md)

-   [Determinar el modo de edición](../../../ado/guide/data/determining-edit-mode.md)

-   [Uso de AddNew de inmediato y modos de lote](../../../ado/guide/data/using-addnew-in-immediate-and-batch-modes.md)
