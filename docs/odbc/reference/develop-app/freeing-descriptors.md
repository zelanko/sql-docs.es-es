---
title: Liberar descriptores | Documentos de Microsoft
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
- SQLFreeHandle function [ODBC]
- descriptors [ODBC], allocating and freeing
- freeing descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 317213f4-0ebb-4bf8-a37a-4d6b1313823f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e99c394521bf6f733503e2d5e2f8794d5412cc94
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="freeing-descriptors"></a>Descriptores de liberación
Pueden ser asignados explícitamente descriptores liberan ya sea explícitamente, mediante una llamada a **SQLFreeHandle** con *HandleType* de SQL_HANDLE_DESC o implícita, cuando se libera el identificador de conexión. Cuando se libera un descriptor asignado explícitamente, todos los identificadores de instrucciones a la que revertir el descriptor liberado aplicado automáticamente a los descriptores de implícitamente asignados.  
  
 Se pueden liberar los descriptores implícitamente asignadas solo mediante una llamada a **SQLDisconnect**, que quita cualquier instrucción o descriptores abrir en la conexión, o mediante una llamada a **SQLFreeHandle** con un  *HandleType* de SQL_HANDLE_STMT para liberar un identificador de instrucción y todos los descriptores de implícitamente asignados asociados a la instrucción. No se puede liberar un descriptor asignado implícitamente mediante una llamada a **SQLFreeHandle** con un *HandleType* de SQL_HANDLE_DESC.  
  
 Incluso cuando se libera, sigue siendo válido, un descriptor asignado implícitamente y **SQLGetDescField** puede llamarse en sus campos.
