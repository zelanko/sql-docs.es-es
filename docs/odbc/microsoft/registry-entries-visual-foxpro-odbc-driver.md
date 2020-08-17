---
description: Entradas del registro (el controlador ODBC de Visual FoxPro)
title: Entradas del registro (controlador ODBC de Visual FoxPro) | Microsoft Docs
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
ms.openlocfilehash: cc4c5d617590e6435d99756b159c6049551d2d69
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340351"
---
# <a name="registry-entries-visual-foxpro-odbc-driver"></a>Entradas del registro (el controlador ODBC de Visual FoxPro)
Al instalar el controlador ODBC de Visual FoxPro, el programa de instalación actualiza el registro del sistema, en la clave del registro HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCInst.ini, para agregar una nueva clave denominada Microsoft Visual FoxPro driver. Bajo esa clave, se agregan los valores descritos en la tabla siguiente.  
  
|Nombre del valor|Tipo de valor|Value|  
|----------------|----------------|-----------|  
|APILevel|REG_SZ|"1"|  
|ConnectFunctions|REG_SZ|"YYN"|  
|Controlador|REG_SZ|Ruta de acceso del sistema al archivo de vfpodbc.dll|  
|DriverODBCVer|REG_SZ|"02,50"|  
|FileExtns|REG_SZ|"*. DBF, \* . CDX, \* . FPT"|  
|FileUsage|REG_SZ|"1"|  
|Configurar|REG_SZ|Ruta de acceso del sistema al archivo de vfpodbc.dll|  
|SQLLevel|REG_SZ|"0"|  
  
 El programa de instalación también agrega la clave "archivos de Visual FoxPro", que representa el controlador de Visual FoxPro predeterminado, a la clave de HKEY_CURRENT_USER\SOFTWARE\ODBC\Odbc.ini del sistema. Bajo esta clave, el programa de instalación agrega los valores descritos en la tabla siguiente.  
  
|Nombre del valor|Tipo de valor|Value|  
|----------------|----------------|-----------|  
|Controlador|REG_SZ|Ruta de acceso del sistema al archivo de vfpodbc.dll|  
  
 Cada vez que se agrega un origen de datos ODBC de Visual FoxPro a la configuración de ODBC, se agrega una nueva clave para ese nombre de origen de datos. Los valores del origen de datos corresponden a los valores establecidos en el cuadro de diálogo **configuración de ODBC Visual FoxPro** , tal como se muestra en la tabla siguiente.  
  
|Nombre del valor (palabra clave)|Tipo de valor|Value|  
|----------------------------|----------------|-----------|  
|Intercalar|REG_SQ|Cualquier secuencia de intercalación admitida|  
|Descripción|REG_SZ|Descripción del origen de datos del usuario|  
|Controlador||Ruta de acceso del sistema al archivo de vfpodbc.dll|  
|Exclusivo||Sí o no|  
|BackgroundFetch||Sí o no|  
|SourceDB|REG_SZ|Ruta de acceso a. Archivo DBC|  
|SourceType|REG_SZ|"DBC" o "DBF"|  
  
 No debe tener acceso a esta información directamente; la administración del registro la controla el administrador de ODBC al agregar, modificar o eliminar un origen de datos.  
  
 Puede utilizar algunas de estas palabras clave y valores como parámetros en la función [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md) de la API de ODBC.
