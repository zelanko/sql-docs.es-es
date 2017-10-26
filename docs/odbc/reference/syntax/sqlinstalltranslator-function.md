---
title: "Función SQLInstallTranslator | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLInstallTranslator
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallTranslator
helpviewer_keywords:
- SQLInstallTranslator function [ODBC]
ms.assetid: 453b21ff-3c2b-4069-8ff7-5c727f062d89
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2b7efa21691627c346b6d3798ade158e946071e6
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlinstalltranslator-function"></a>SQLInstallTranslator (función)
**Conformidad**  
 Versión introdujo: ODBC 2.5, en desuso  
  
 **Resumen**  
 En ODBC 3.0, **SQLInstallTranslator** se ha reemplazado por [SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md). Las llamadas a **SQLInstallTranslator** se asignarán a **SQLInstallTranslatorEx**. Para obtener más información, consulte **SQLInstallTranslatorEx**.  
  
 **SQLInstallTranslator** devolverá FALSE si una aplicación llama en ODBC 3*.x* el Administrador de controladores con el *lpszInfFile* establecido en un valor distinto de NULL. El archivo de ODBC usado en ODBC 2. *x* ya no se admite en ODBC 3*.x*, ni siquiera para compatibilidad con versiones anteriores.

