---
title: Enlazar registros descriptores | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- bound descriptor records [ODBC]
- descriptors [ODBC], bound descriptor records
ms.assetid: 55d09344-6682-40f6-b634-036b134ff650
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d1e7c9c3d93403515c118757a6a947a6b5a68b9c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="bound-descriptor-records"></a>Registros de Descriptor de enlace
Cuando la aplicación establece el campo SQL_DESC_DATA_PTR de un registro de descriptor para que ya no contiene un valor null, se dice que el registro sea *enlazados*.  
  
 Si el descriptor es un APD, cada registro enlazado constituye un parámetro enlazado. Para los parámetros de entrada, la aplicación debe enlazar un parámetro para cada marcador de parámetro dinámico en la instrucción SQL antes de ejecutar la instrucción. Para los parámetros de salida, la aplicación no necesita enlazar el parámetro.  
  
 Si el descriptor es un descartar, que describe una fila de la base de datos, cada registro enlazado constituye una columna enlazada.
