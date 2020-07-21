---
title: Asignar el cursor Attributes1 tipos de información | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], mapping cursor attributes1 information types
- application upgrades [ODBC], mapping cursor attributes1 information types
- mapping cursor attributes1 information types [ODBC]
- backward compatibility [ODBC], mapping cursor attributes1 information types
- upgrading applications [ODBC], mapping cursor attributes1 information types
ms.assetid: 9f112449-ca86-45ac-a865-e6174d67f91b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d70cf0a93a6c6160faeb0afe991b2adfff11b8f1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301048"
---
# <a name="mapping-the-cursor-attributes1-information-types"></a>Asignar los tipos de información de Cursor Attributes1
Cuando se trata de un ODBC 3. la aplicación *x* llama a **SQLGetInfo** en un controlador ODBC 2 *. x* con el tipo de información SQL_XXXX_CURSOR_ATTRIBUTES1 (para cursores dinámicos, de solo avance, de controlador de conjunto de claves o estáticos), la configuración de los bits devueltos por el administrador de controladores depende del ODBC 2. el controlador *x* devuelve para el ODBC 2 correspondiente. tipos de información *x* . Los bits se establecen como se muestra en la tabla siguiente.  
  
|Bit en<br /><br /> SQL_XXXX_CURSOR_ATTRIBUTES1|Tipo de cursor|ODBC 2. información de *x*<br /><br /> type|  
|-----------------------------------------------|-----------------|-------------------------------------|  
|SQL_CA1_NEXT|All|SQL_FETCH_DIRECTION|  
|SQL_CA1_ABSOLUTE SQL_CA1_RELATIVE SQL_CA1_BOOKMARK|Dinámico, controlador de conjunto de claves, estático|SQL_FETCH_DIRECTION|  
|SQL_CA1_LOCK_NO_CHANGE SQL_CA1_LOCK_UNLOCK SQL_CA1_LOCK_EXCLUSIVE|Dinámico, controlador de conjunto de claves, estático|SQL_LOCK_TYPES|  
|SQL_CA1_POSITIONED_UPDATE SQL_CA1_POSITIONED_DELETE SQL_CA1_SELECT_FOR_UPDATE|All|SQL_POSITIONED_STATEMENTS|  
|SQL_CA1_POS_POSITION SQL_CA1_POS_DELETE SQL_CA1_POS_REFRESH SQL_CA1_POS_BULK_ADD|Dinámico, controlador de conjunto de claves, estático|SQL_POS_OPERATIONS|
