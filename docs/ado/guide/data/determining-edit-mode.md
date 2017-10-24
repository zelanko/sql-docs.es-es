---
title: "Determinar el modo de edición | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- editing data [ADO], edit mode
- ADO, editing data
ms.assetid: 4c7e010d-08cd-4e22-9b32-23c36f02f88c
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ca4098a61984e009a2874fdca55d898938ce702d
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="determining-edit-mode"></a>Determinar el modo de edición
ADO mantiene un búfer de edición asociado al registro actual. El **EditMode** propiedad indica si se realizaron cambios en este búfer o si se ha creado un nuevo registro. Use **EditMode** para determinar el estado de edición del registro actual. Puede probar cambios pendientes si un proceso de modificación se ha interrumpido y determinar si necesita usar el **actualización** o **CancelUpdate** método.  
  
 **EditMode** devuelve uno de los **EditModeEnum** constantes, que se enumeran en la tabla siguiente.  
  
|Constante|Description|  
|--------------|-----------------|  
|**adEditNone**|No indica que no hay ninguna operación de edición en curso.|  
|**adEditInProgress**|Indica que se ha modificado pero no se guardan los datos en el registro actual.|  
|**adEditAdd**|Indica que la **AddNew** ha llamado al método y el registro actual en el búfer de copia es un nuevo registro que no se ha guardado en la base de datos.|  
|**adEditDelete**|Indica que se ha eliminado el registro actual.|  
  
 **EditMode** puede devolver un valor válido únicamente si hay un registro actual. **EditMode** devolverá un error si **BOF** o **EOF** es **True** o si se ha eliminado el registro actual.

