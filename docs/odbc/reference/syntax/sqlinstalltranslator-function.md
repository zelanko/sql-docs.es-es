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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b094aa730fff6db80b9addb63a92bee0f5f85b2a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300325"
---
# <a name="sqlinstalltranslator-function"></a>Función SQLInstallTranslator
**Conformidad**  
 Versión introducida: ODBC 2,5, en desuso  
  
 **Resumen**  
 En ODBC 3,0, **SQLInstallTranslator** se ha reemplazado por [SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md). Las llamadas a **SQLInstallTranslator** se asignarán a **SQLInstallTranslatorEx**. Para obtener más información, vea **SQLInstallTranslatorEx**.  
  
 **SQLInstallTranslator** devolverá FALSE si una aplicación la llama en el administrador de controladores ODBC *3. x* con el argumento *lpszInfFile* establecido en un valor distinto de NULL. El archivo ODBC. inf que se usa en ODBC *2. x* ya no se admite en ODBC *3. x*, incluso para mantener la compatibilidad con versiones anteriores.
