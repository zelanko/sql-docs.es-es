---
title: Resumen de funciones DLL de instalador | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], installer DLL functions
- installer DLL [ODBC]
ms.assetid: 666c09d3-1e10-4d89-9b42-eda2957a87f0
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 22affac7219620f0f7caaf2ea8d4affdb91666ce
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="installer-dll-function-summary"></a>Resumen de funciones DLL de instalador
En la tabla siguiente describe las funciones en el archivo DLL del instalador. Para obtener más información sobre la sintaxis y semántica para cada función, consulte [referencia API DLL del instalador](../../../odbc/reference/syntax/installer-dll-api-reference-function.md).  
  
|Tarea|Nombre de función|Finalidad|  
|----------|-------------------|-------------|  
|Instalar ODBC|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|Carga el archivo DLL de configuración específicos del controlador.|  
||[SQLGetInstalledDrivers](../../../odbc/reference/syntax/sqlgetinstalleddrivers-function.md)|Devuelve una lista de controladores instalados.|  
||[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|Agrega un controlador a la información del sistema.|  
||[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|Devuelve el directorio de destino para el Administrador de controladores.|  
||[SQLInstallerError](../../../odbc/reference/syntax/sqlinstallererror-function.md)|Devuelve información de estado o de error para las funciones del instalador.|  
||[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|Agrega un traductor a la información del sistema.|  
||[SQLPostInstallerError](../../../odbc/reference/syntax/sqlpostinstallererror-function.md)|Permite que una biblioteca del programa de instalación de controlador o traductor para informar de errores.|  
||[SQLRemoveDriver](../../../odbc/reference/syntax/sqlremovedriver-function.md)|Quita un controlador de la información del sistema.|  
||[SQLRemoveDriverManager](../../../odbc/reference/syntax/sqlremovedrivermanager-function.md)|Quita los componentes principales de ODBC de la información del sistema.|  
||[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|Quita el traductor de la información del sistema.|  
|Configurar orígenes de datos|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|Llama a la DLL de configuración específicos del controlador.|  
||[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|Muestra un cuadro de diálogo para agregar un origen de datos.|  
||[SQLGetConfigMode](../../../odbc/reference/syntax/sqlgetconfigmode-function.md)|Recupera el modo de configuración que indica que la entrada de Odbc.ini enumerar valores DSN en la información del sistema.|  
||[SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|Escribe un valor en la información del sistema.|  
||[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|Muestra un cuadro de diálogo para seleccionar un traductor.|  
||[SQLManageDataSources](../../../odbc/reference/syntax/sqlmanagedatasources.md)|Muestra un cuadro de diálogo para configurar controladores y orígenes de datos.|  
||[SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)|Lee información de DSN de archivo.|  
||[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|Quita el origen de datos predeterminado.|  
||[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|Quita un origen de datos.|  
||[SQLSetConfigMode](../../../odbc/reference/syntax/sqlsetconfigmode-function.md)|Establece el modo de configuración que indica que la entrada de Odbc.ini enumerar valores DSN en la información del sistema.|  
||[SQLValidDSN](../../../odbc/reference/syntax/sqlvaliddsn-function.md)|Comprueba la longitud y la validez del nombre del origen de datos.|  
||[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|Agrega un origen de datos.|  
||[SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)|Escribe información en el DSN de archivo.|  
||[SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|Obtiene un valor de la información del sistema.|
