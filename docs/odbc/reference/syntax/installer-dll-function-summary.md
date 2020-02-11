---
title: Resumen de la función DLL del instalador | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], installer DLL functions
- installer DLL [ODBC]
ms.assetid: 666c09d3-1e10-4d89-9b42-eda2957a87f0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e6d2a865764a3d802a7e5a5341226d7d1aa855f5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68095683"
---
# <a name="installer-dll-function-summary"></a>Resumen de funciones DLL de instalador
En la tabla siguiente se describen las funciones de la DLL del instalador. Para obtener más información sobre la sintaxis y la semántica de cada función, vea referencia de la [API de dll del instalador](../../../odbc/reference/syntax/installer-dll-api-reference-function.md).  
  
|Tarea|Nombre de función|Propósito|  
|----------|-------------------|-------------|  
|Instalar ODBC|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|Carga el archivo DLL de instalación específico del controlador.|  
||[SQLGetInstalledDrivers](../../../odbc/reference/syntax/sqlgetinstalleddrivers-function.md)|Devuelve una lista de los controladores instalados.|  
||[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|Agrega un controlador a la información del sistema.|  
||[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|Devuelve el directorio de destino para el administrador de controladores.|  
||[SQLInstallerError](../../../odbc/reference/syntax/sqlinstallererror-function.md)|Devuelve información de error o de estado de las funciones del instalador.|  
||[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|Agrega un traductor a la información del sistema.|  
||[SQLPostInstallerError](../../../odbc/reference/syntax/sqlpostinstallererror-function.md)|Permite que un controlador o una biblioteca de instalación de Translator informe de errores.|  
||[SQLRemoveDriver](../../../odbc/reference/syntax/sqlremovedriver-function.md)|Quita un controlador de la información del sistema.|  
||[SQLRemoveDriverManager](../../../odbc/reference/syntax/sqlremovedrivermanager-function.md)|Quita los componentes principales de ODBC de la información del sistema.|  
||[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|Quita el traductor de la información del sistema.|  
|Configuración de orígenes de datos|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|Llama al archivo DLL de instalación específico del controlador.|  
||[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|Muestra un cuadro de diálogo para agregar un origen de datos.|  
||[SQLGetConfigMode](../../../odbc/reference/syntax/sqlgetconfigmode-function.md)|Recupera el modo de configuración que indica dónde se encuentra la entrada ODBC. ini que enumera los valores DSN en la información del sistema.|  
||[SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|Escribe un valor en la información del sistema.|  
||[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|Muestra un cuadro de diálogo para seleccionar un traductor.|  
||[SQLManageDataSources](../../../odbc/reference/syntax/sqlmanagedatasources.md)|Muestra un cuadro de diálogo para configurar los orígenes de datos y los controladores.|  
||[SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)|Lee información de los DSN de archivo.|  
||[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|Quita el origen de datos predeterminado.|  
||[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|Quita un origen de datos.|  
||[SQLSetConfigMode](../../../odbc/reference/syntax/sqlsetconfigmode-function.md)|Establece el modo de configuración que indica dónde se encuentra la entrada ODBC. ini que enumera los valores DSN en la información del sistema.|  
||[SQLValidDSN](../../../odbc/reference/syntax/sqlvaliddsn-function.md)|Comprueba la longitud y la validez del nombre del origen de datos.|  
||[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|Agrega un origen de datos.|  
||[SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)|Escribe información en los DSN de archivo.|  
||[SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|Obtiene un valor de la información del sistema.|
