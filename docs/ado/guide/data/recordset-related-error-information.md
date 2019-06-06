---
title: Información de Error relacionado con el conjunto de registros | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset-related errors [ADO]
- errors [ADO], Recordset-related
ms.assetid: 7e103574-59ad-4790-b5f9-fa8d715e711e
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ef5f6cc4a262cecc81a8dd72f2d3e3f6a7e2fded
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66700412"
---
# <a name="recordset-related-error-information"></a>Información de Error relacionado con el conjunto de registros
Durante el procesamiento por lotes, el **estado** propiedad de la **Recordset** objeto proporciona información sobre los registros individuales de la **Recordset**. Antes de que una actualización por lotes, el **estado** propiedad de la **Recordset** refleja información acerca de los registros para agregar, cambiar y eliminar. Después de **UpdateBatch** se ha llamado el **estado** propiedad indica el éxito o fracaso de la operación. Mientras se desplaza por los registros en el **Recordset**, el valor de la **estado** los cambios de propiedad para describir el estado del registro actual.
