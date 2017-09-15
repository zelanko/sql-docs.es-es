---
title: SQLTransact (controlador de acceso) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Access driver [ODBC], SQLTransact
- SQLTransact function [ODBC], Access Driver
ms.assetid: 892b79c7-9e20-4d1f-bc60-d4b25694ca25
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 657d0324132b279300e2a61151c790f066e4a3f5
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqltransact-access-driver"></a>SQLTransact (controlador de Access)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de acceso. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Cuando se utiliza el controlador de Microsoft Access, SQL_COMMIT o SQL_ROLLBACK se admiten para la *fType* argumento en una llamada a **SQLTransact**.  
  
 Si se produce un error durante el proceso de confirmación, se puede reparar la base de datos mediante la opción de base de datos de reparación en el programa de instalación del controlador de Microsoft Access, o mediante el uso de la palabra clave REPAIR_DB en el **SQLConfigDataSource** función.
