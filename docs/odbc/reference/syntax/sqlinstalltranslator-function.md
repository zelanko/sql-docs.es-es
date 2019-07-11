---
title: Función SQLInstallTranslator | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 08a9e3a1afef8b9ea3bf1f4266196341e0edeb76
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2019
ms.locfileid: "67792863"
---
# <a name="sqlinstalltranslator-function"></a>Función SQLInstallTranslator
**Conformidad**  
 Versión de introducción: ODBC 2.5, en desuso  
  
 **Resumen**  
 En ODBC 3.0, **SQLInstallTranslator** ha sido reemplazado por [SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md). Las llamadas a **SQLInstallTranslator** se asignará a **SQLInstallTranslatorEx**. Para obtener más información, consulte **SQLInstallTranslatorEx**.  
  
 **SQLInstallTranslator** devolverá FALSE si una aplicación lo llama en ODBC *3.x* Administrador de controladores con el *lpszInfFile* argumento establecido en un valor distinto de NULL. El archivo de ODBC usado en ODBC *2.x* ya no se admite en ODBC *3.x*, incluso para compatibilidad con versiones anteriores.
