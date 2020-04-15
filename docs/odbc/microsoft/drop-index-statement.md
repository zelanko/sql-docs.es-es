---
title: Instrucción DROP INDEX (Drop INDEX) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DROP INDEX [ODBC]
- SQL grammar [ODBC], DROP INDEX
ms.assetid: cd0ff767-9254-413b-bd1a-bed26c6774f5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 638bae6491c020519a0123ff56fe31e9a9ca1cf7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303436"
---
# <a name="drop-index-statement"></a>Instrucción DROP INDEX
Cuando se utiliza el controlador Microsoft Access, dBASE o Paradox, la sintaxis de la instrucción DROP INDEX es "DROP INDEX a on b" donde "a" es el nombre del índice y "b" es el nombre de la tabla (no DROP INDEX *index-name*).  
  
 Cuando se utiliza el controlador Paradox, la instrucción DROP INDEX elimina los archivos de índice secundario de Paradox.  
  
 La instrucción DROP INDEX no se admite para los controladores de Microsoft Excel o Text.
