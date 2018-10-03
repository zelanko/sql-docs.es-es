---
title: Determinar el modo de edición | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- editing data [ADO], edit mode
- ADO, editing data
ms.assetid: 4c7e010d-08cd-4e22-9b32-23c36f02f88c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e638cda03d7dc0f0bd580c3ca29c126568d1595a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47705243"
---
# <a name="determining-edit-mode"></a>Determinar el modo de edición
ADO mantiene un búfer de edición asociado con el registro actual. El **EditMode** propiedad indica si se han realizado cambios a este búfer, o si se ha creado un nuevo registro. Use **EditMode** para determinar el estado de edición del registro actual. Puede probar cambios pendientes si un proceso de edición se ha interrumpido y determinar si necesita usar el **actualización** o **CancelUpdate** método.  
  
 **EditMode** devuelve uno de los **EditModeEnum** constantes, que se muestran en la tabla siguiente.  
  
|Constante|Descripción|  
|--------------|-----------------|  
|**adEditNone**|Indica que no hay ninguna operación de edición está en curso.|  
|**adEditInProgress**|Indica que los datos en el registro actual se ha modificado pero no guardado.|  
|**adEditAdd**|Indica que el **AddNew** ha llamado al método y el registro actual en el búfer de copia es un nuevo registro que no se ha guardado en la base de datos.|  
|**adEditDelete**|Indica que se ha eliminado el registro actual.|  
  
 **EditMode** puede devolver un valor válido solo si hay un registro actual. **EditMode** devolverá un error si **BOF** o **EOF** es **True** o si se ha eliminado el registro actual.
