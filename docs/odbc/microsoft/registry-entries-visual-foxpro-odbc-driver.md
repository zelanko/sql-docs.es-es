---
title: Entradas del Registro (Controlador ODBC de Visual FoxPro) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- registry keys [ODBC]
- Visual FoxPro ODBC driver [ODBC], registry entries
- keys [ODBC]
- FoxPro ODBC driver [ODBC], registry entries
ms.assetid: 1a63d92d-ca3a-46ae-911f-6788292c801e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bd2d419a94c45a872789e095b014159b41d7c217
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304842"
---
# <a name="registry-entries-visual-foxpro-odbc-driver"></a>Entradas del registro (el controlador ODBC de Visual FoxPro)
Al instalar el controlador ODBC de Visual FoxPro, el programa de instalación actualiza el registro del sistema, en la clave del Registro HKEY_LOCAL_MACHINE, SOFTWARE, ODBC, ODBCInst.ini, para agregar una nueva clave denominada Controlador de Microsoft Visual FoxPro. Bajo esa clave, se agregan los valores descritos en la tabla siguiente.  
  
|Nombre del valor|Tipo de valor|Value|  
|----------------|----------------|-----------|  
|APILevel|REG_SZ|"1"|  
|ConnectFunctions|REG_SZ|"YYN"|  
|Controlador|REG_SZ|Ruta del sistema al archivo vfpodbc.dll|  
|DriverODBCVer|REG_SZ|"02.50"|  
|FileExtns|REG_SZ|"*.dbf,\*.cdx,\*.fpt"|  
|Fileusage|REG_SZ|"1"|  
|Configurar|REG_SZ|Ruta del sistema al archivo vfpodbc.dll|  
|SQLLevel|REG_SZ|"0"|  
  
 El programa de instalación también agrega la clave "Visual FoxPro Files", que representa el controlador predeterminado de Visual FoxPro, a la clave HKEY_CURRENT_USER de su sistema. Bajo esta clave, el programa de instalación agrega los valores descritos en la tabla siguiente.  
  
|Nombre del valor|Tipo de valor|Value|  
|----------------|----------------|-----------|  
|Controlador|REG_SZ|Ruta del sistema al archivo vfpodbc.dll|  
  
 Cada vez que se agrega un origen de datos ODBC de Visual FoxPro a la configuración ODBC, se agrega una nueva clave para ese nombre de origen de datos. Los valores del origen de datos corresponden a los valores establecidos en el cuadro de diálogo Configuración de **ODBC Visual FoxPro,** como se muestra en la tabla siguiente.  
  
|Nombre del valor (palabra clave)|Tipo de valor|Value|  
|----------------------------|----------------|-----------|  
|Intercalar|REG_SQ|Cualquier secuencia de intercalación compatible|  
|Descripción|REG_SZ|Descripción del usuario de la fuente de datos|  
|Controlador||Ruta del sistema al archivo vfpodbc.dll|  
|Exclusivo||Sí o no|  
|BackgroundFetch||Sí o no|  
|SourceDB|REG_SZ|Ruta de acceso a . Archivo DBC|  
|SourceType|REG_SZ|"DBC" o "DBF"|  
  
 No debe acceder a esta información directamente; Cualquier administración del registro la controla el Administrador ODBC al agregar, modificar o eliminar un origen de datos.  
  
 Puede usar algunas de estas palabras clave y valores como parámetros en la función de API ODBC de [SQLDriverConnect.](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)
