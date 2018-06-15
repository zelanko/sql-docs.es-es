---
title: Liberar descriptores | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
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
ms.openlocfilehash: 4c96d5b654d8331f95e3abbe8a3aa8b563bf7a63
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32911580"
---
# <a name="freeing-descriptors"></a>Descriptores de liberación
Pueden ser asignados explícitamente descriptores liberan ya sea explícitamente, mediante una llamada a **SQLFreeHandle** con *HandleType* de SQL_HANDLE_DESC o implícita, cuando se libera el identificador de conexión. Cuando se libera un descriptor asignado explícitamente, todos los identificadores de instrucciones a la que revertir el descriptor liberado aplicado automáticamente a los descriptores de implícitamente asignados.  
  
 Se pueden liberar los descriptores implícitamente asignadas solo mediante una llamada a **SQLDisconnect**, que quita cualquier instrucción o descriptores abrir en la conexión, o mediante una llamada a **SQLFreeHandle** con un  *HandleType* de SQL_HANDLE_STMT para liberar un identificador de instrucción y todos los descriptores de implícitamente asignados asociados a la instrucción. No se puede liberar un descriptor asignado implícitamente mediante una llamada a **SQLFreeHandle** con un *HandleType* de SQL_HANDLE_DESC.  
  
 Incluso cuando se libera, sigue siendo válido, un descriptor asignado implícitamente y **SQLGetDescField** puede llamarse en sus campos.
