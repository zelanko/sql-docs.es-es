---
title: Editar los registros existentes | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ce8679c0c7b20dfaa641918f0447a2f77bfd474a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925436"
---
# <a name="editing-existing-records"></a>Editar los registros existentes
Para editar los registros existentes, vaya a la fila que desea editar y cambiar el **valor** propiedad de los campos que desee cambiar. Para obtener más información sobre la **campo** del objeto **valor** propiedad, vea [examinar datos](../../../ado/guide/data/examining-data.md). Dependiendo del tipo de cursor, se utilizará **actualización** o **UpdateBatch** para enviar los cambios en el origen de datos. Para obtener más información, consulte [actualizar y conservar datos](../../../ado/guide/data/updating-and-persisting-data.md).  
  
 Es normalmente más eficaz utilizar un procedimiento almacenado con un objeto de comando para realizar actualizaciones, así como para realizar otras operaciones, porque un procedimiento almacenado no requiere la creación de un cursor. Para obtener más información acerca de los cursores, vea [cursores y bloqueos](../../../ado/guide/data/understanding-cursors-and-locks.md).
