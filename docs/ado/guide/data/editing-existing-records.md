---
title: Editando registros existentes | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- editing data [ADO], existing records
ms.assetid: 17ce1263-5897-452a-9ea5-c7f96b33df65
author: rothja
ms.author: jroth
ms.openlocfilehash: 71d8b825766ca94984ca2dc0b51577488178920f
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761031"
---
# <a name="editing-existing-records"></a>Editar los registros existentes
Para editar los registros existentes, desplácese a la fila que desea editar y cambie la propiedad **valor** de los campos que desee cambiar. Para obtener más información sobre la propiedad **Value** del objeto de **campo** , vea [examinar datos](../../../ado/guide/data/examining-data.md). Dependiendo del tipo de cursor, utilizará **Update** o **UpdateBatch** para devolver los cambios al origen de datos. Para obtener más información, vea [actualizar y conservar datos](../../../ado/guide/data/updating-and-persisting-data.md).  
  
 Normalmente es más eficaz usar un procedimiento almacenado con un objeto de comando para realizar actualizaciones, así como para realizar otras operaciones, porque un procedimiento almacenado no requiere la creación de un cursor. Para obtener más información sobre los cursores, vea Descripción de los [cursores y bloqueos](../../../ado/guide/data/understanding-cursors-and-locks.md).
