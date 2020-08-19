---
description: Información de Error relacionado con el conjunto de registros
title: Información de error relacionada con el conjunto de registros | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 7806d446c200f4d90ec458ceea268435ad9994e1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452957"
---
# <a name="recordset-related-error-information"></a>Información de Error relacionado con el conjunto de registros
Durante el procesamiento por lotes, la propiedad **status** del objeto de **conjunto de registros** proporciona información sobre los registros individuales del **conjunto de registros**. Antes de que tenga lugar una actualización por lotes, la propiedad **status** del **conjunto de registros** refleja información acerca de los registros que se van a agregar, modificar y eliminar. Después de llamar a **UpdateBatch** , la propiedad **status** indica si la operación se ha realizado correctamente o no. A medida que se mueve de un registro a otro en el **conjunto de registros**, el valor de la propiedad **status** cambia para describir el estado del registro actual.
