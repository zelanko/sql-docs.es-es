---
title: Asigna explícitamente descriptores | Documentos de Microsoft
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
- descriptors [ODBC], allocating and freeing
- explicitly allocated descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: f590251d-56a6-4d58-a405-9e85e68fbc47
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5f92ad0615047da9fd775ec8faa491e8d9a4ba79
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="explicitly-allocated-descriptors"></a>Descriptores asignados explícitamente
Una aplicación puede asignar explícitamente un descriptor de la aplicación en una conexión en cualquier momento en que está conectado a la base de datos. Especificando este identificador de descriptor como un atributo de una instrucción controlar mediante **SQLSetStmtAttr**, la aplicación indica al controlador que use ese descriptor en lugar de los correspondientes asigna implícitamente la aplicación descriptores. La aplicación no puede especificar descriptores de implementación alternativa.  
  
 Una aplicación puede asociar un descriptor asignado explícitamente a más de una instrucción. Cuando una aplicación realmente esté conectada a la base de datos puede ser un descriptor de un descriptor asignado explícitamente. La aplicación puede liberar un descriptor de tal explícita o implícitamente al liberar la conexión.
