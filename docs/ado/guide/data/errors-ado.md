---
description: Errores (ADO)
title: Errores (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB providers [ADO]
- ADO, OLE DB providers
ms.assetid: 8ae6611b-3069-4155-b014-c0c9da37be39
author: rothja
ms.author: jroth
ms.openlocfilehash: 392d1f2fdfc0a7fe2e0cf9e1e14efb77f396acfd
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806125"
---
# <a name="errors-ado"></a>Errores (ADO)
Cualquier operación relacionada con objetos ADO puede generar uno o más errores de proveedor. Cuando se produce cada error, se colocan uno o varios objetos de **error** en la colección de **errores** del objeto de **conexión** . Para obtener más información sobre cómo controlar las advertencias y los errores de la aplicación ADO, vea [control de errores](./error-handling.md).  
  
 Los errores de aplicación se pueden generar mediante un mecanismo independiente. Por ejemplo, en Visual Basic, el objeto **Err** contendrá errores en el nivel de la aplicación.