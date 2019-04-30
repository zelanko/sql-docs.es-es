---
title: Enlaza los registros descriptores | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- bound descriptor records [ODBC]
- descriptors [ODBC], bound descriptor records
ms.assetid: 55d09344-6682-40f6-b634-036b134ff650
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6f7d21a1166868603f9389ab4ef5c5b3448b0312
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63199523"
---
# <a name="bound-descriptor-records"></a>Registros de Descriptor de enlace
Cuando la aplicación establece el campo SQL_DESC_DATA_PTR de un registro de descriptor para que ya no contiene un valor null, el registro se dice que *enlazados*.  
  
 Si el descriptor no es un APD, cada registro enlazado constituye un parámetro dependiente. Parámetros de entrada, la aplicación debe enlazar un parámetro para cada marcador de parámetro dinámico en la instrucción SQL antes de ejecutar la instrucción. Para los parámetros de salida, la aplicación no necesita enlazar el parámetro.  
  
 Si el descriptor es un descartar, que describe una fila de la base de datos, cada registro enlazado constituye una columna enlazada.
