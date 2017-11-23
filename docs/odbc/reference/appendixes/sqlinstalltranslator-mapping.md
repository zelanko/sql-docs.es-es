---
title: "Asignación de SQLInstallTranslator | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLInstallTranslator function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLInstallTranslator
ms.assetid: bcd9ba4f-7834-4bc4-876e-c7478998e524
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cb17f3d77b39c43d1f20c4598ac0192332a9cf13
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="sqlinstalltranslator-mapping"></a>Asignación de SQLInstallTranslator
Cuando un ODBC 2. *x* aplicación llama **SQLInstallTranslator** a través de una aplicación ODBC 3*.x* controlador, el Administrador de controladores asigna la llamada a **SQLInstallTranslatorEx**. Una aplicación no debe llamar a **SQLInstallTranslator** en ODBC 3*.x* el Administrador de controladores con el *lpszInfFile* establecido en un valor distinto de NULL. El SDK de ODBC. Archivo INF utilizada en ODBC 2. *x* ya no se admite en ODBC 3*.x*, ni siquiera para compatibilidad con versiones anteriores.
