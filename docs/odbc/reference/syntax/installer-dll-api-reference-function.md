---
title: Función de referencia de la API de DLL de instalador | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installer DLL [ODBC]
ms.assetid: 47fcadc3-f102-4989-9ee7-a1c65233142a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 14a89c859e98a069106b79c9289187a64c310fa9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63232820"
---
# <a name="installer-dll-api-reference-function"></a>Función de referencia de API de DLL de instalador
En esta sección se describe la sintaxis de las funciones en el instalador de la API de DLL. El instalador de la API de DLL se compone de 20 funciones. Tres de estas funciones, **SQLGetTranslator**, **SQLRemoveDSNFromIni**, y **SQLWriteDSNToIni**, solo llama a las DLL de instalación. Las demás funciones son llamadas por los programas de instalación y administración.  
  
 Cada función se etiqueta con la versión de ODBC en el que se introdujo.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Función SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)  
  
-   [Función SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)  
  
-   [Función SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)  
  
-   [Función SQLGetConfigMode](../../../odbc/reference/syntax/sqlgetconfigmode-function.md)  
  
-   [Función SQLGetInstalledDrivers](../../../odbc/reference/syntax/sqlgetinstalleddrivers-function.md)  
  
-   [Función SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)  
  
-   [Función SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)  
  
-   [Función SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)  
  
-   [Función SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)  
  
-   [Función SQLInstallerError](../../../odbc/reference/syntax/sqlinstallererror-function.md)  
  
-   [Función SQLInstallTranslator](../../../odbc/reference/syntax/sqlinstalltranslator-function.md)  
  
-   [Función SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)  
  
-   [Función SQLManageDataSources](../../../odbc/reference/syntax/sqlmanagedatasources.md)  
  
-   [Función SQLPostInstallerError](../../../odbc/reference/syntax/sqlpostinstallererror-function.md)  
  
-   [Función SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)  
  
-   [Función SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)  
  
-   [Función SQLRemoveDriver](../../../odbc/reference/syntax/sqlremovedriver-function.md)  
  
-   [Función SQLRemoveDriverManager](../../../odbc/reference/syntax/sqlremovedrivermanager-function.md)  
  
-   [Función SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)  
  
-   [Función SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)  
  
-   [Función SQLSetConfigMode](../../../odbc/reference/syntax/sqlsetconfigmode-function.md)  
  
-   [Función SQLValidDSN](../../../odbc/reference/syntax/sqlvaliddsn-function.md)  
  
-   [Función SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)  
  
-   [Función SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)  
  
-   [Función SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)
