---
title: "Información de Error relacionado con el conjunto de registros | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Recordset-related errors [ADO]
- errors [ADO], Recordset-related
ms.assetid: 7e103574-59ad-4790-b5f9-fa8d715e711e
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9acefac1018525813644fedf011dea5a95cb875f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="recordset-related-error-information"></a>Información de Error relacionado con el conjunto de registros
Durante el procesamiento por lotes, el **estado** propiedad de la **Recordset** objeto proporciona información acerca de los registros individuales en la **conjunto de registros**. Antes de una actualización por lotes tiene lugar, el **estado** propiedad de la **Recordset** refleja la información acerca de los registros para agregar, cambiar y eliminar. Después de **UpdateBatch** se ha llamado, el **estado** propiedad indica el éxito o fracaso de la operación. Mientras se desplaza por los registros en la **Recordset**, el valor de la **estado** cambios de propiedad para describir el estado del registro actual.
