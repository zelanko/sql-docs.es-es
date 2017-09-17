---
title: Entradas del registro (el controlador ODBC de Visual FoxPro) | Documentos de Microsoft
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
- registry keys [ODBC]
- Visual FoxPro ODBC driver [ODBC], registry entries
- keys [ODBC]
- FoxPro ODBC driver [ODBC], registry entries
ms.assetid: 1a63d92d-ca3a-46ae-911f-6788292c801e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6a975ff73eb4b2ef48af05ccfdf595ae9c3233f0
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="registry-entries-visual-foxpro-odbc-driver"></a>Entradas del registro (el controlador ODBC de Visual FoxPro)
Cuando se instala el controlador ODBC de Visual FoxPro, el programa de instalación actualiza el registro del sistema, en la clave del registro HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCInst.ini, para agregar una nueva clave denominada Microsoft Visual FoxPro Driver. Bajo esa clave, se agregan los valores descritos en la tabla siguiente.  
  
|Nombre del valor|Tipo de valor|Valor|  
|----------------|----------------|-----------|  
|APILevel|REG_SZ|"1"|  
|ConnectFunctions|REG_SZ|"YYN"|  
|Controlador|REG_SZ|Ruta de acceso del sistema en el archivo vfpodbc.dll|  
|DriverODBCVer|REG_SZ|"02.50"|  
|FileExtns|REG_SZ|"*.dbf,\*.cdx,\*.fpt"|  
|FileUsage|REG_SZ|"1"|  
|ssNoVersion|REG_SZ|Ruta de acceso del sistema en el archivo vfpodbc.dll|  
|SQLLevel|REG_SZ|"0"|  
  
 El programa de instalación también agrega la clave "Visual FoxPro Files", que representa el controlador de Visual FoxPro de forma predeterminada, para la clave de HKEY_CURRENT_USER\SOFTWARE\ODBC\Odbc.ini de su sistema. Bajo esta clave, el programa de instalación agrega los valores descritos en la tabla siguiente.  
  
|Nombre del valor|Tipo de valor|Valor|  
|----------------|----------------|-----------|  
|Controlador|REG_SZ|Ruta de acceso del sistema en el archivo vfpodbc.dll|  
  
 Cada vez que agregue un origen de datos ODBC de Visual FoxPro a la configuración de ODBC, se agrega una nueva clave para ese nombre de origen de datos. Los valores del origen de datos corresponden a los valores establecidos en el **programa de instalación de Visual FoxPro ODBC** cuadro de diálogo, como se muestra en la tabla siguiente.  
  
|Nombre del valor (palabra clave)|Tipo de valor|Valor|  
|----------------------------|----------------|-----------|  
|Intercalar|REG_SQ|Cualquier secuencia de intercalación de admitido|  
|Description|REG_SZ|Descripción de usuario del origen de datos|  
|Controlador||Ruta de acceso del sistema en el archivo vfpodbc.dll|  
|Exclusivo||Sí o no|  
|BackgroundFetch||Sí o no|  
|SourceDB|REG_SZ|Ruta de acceso. Archivo DBC|  
|Tipo de origen|REG_SZ|"DBC" o "DBF"|  
  
 No debe tener acceso a esta información directamente; cualquier administración del registro se controla mediante el Administrador de ODBC al agregar, modificar o eliminar un origen de datos.  
  
 Se pueden utilizar algunas de estas palabras clave y los valores como parámetros en la [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md) función de la API de ODBC.
