---
description: Editar los registros existentes
title: Editando registros existentes | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- editing data [ADO], existing records
ms.assetid: 17ce1263-5897-452a-9ea5-c7f96b33df65
author: rothja
ms.author: jroth
ms.openlocfilehash: 35c2376031e96a19c4a761a9826e47be2306518e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991336"
---
# <a name="editing-existing-records"></a>Editar los registros existentes
Para editar los registros existentes, desplácese a la fila que desea editar y cambie la propiedad **valor** de los campos que desee cambiar. Para obtener más información sobre la propiedad **Value** del objeto de **campo** , vea [examinar datos](./examining-data.md). Dependiendo del tipo de cursor, utilizará **Update** o **UpdateBatch** para devolver los cambios al origen de datos. Para obtener más información, vea [actualizar y conservar datos](./updating-and-persisting-data.md).  
  
 Normalmente es más eficaz usar un procedimiento almacenado con un objeto de comando para realizar actualizaciones, así como para realizar otras operaciones, porque un procedimiento almacenado no requiere la creación de un cursor. Para obtener más información sobre los cursores, vea Descripción de los [cursores y bloqueos](./understanding-cursors-and-locks.md).