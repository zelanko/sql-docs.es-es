---
description: Opciones de configuración mediante programación para el controlador de acceso
title: Establecer opciones mediante programación para el controlador de acceso | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], Access driver
- Jet-based ODBC drivers [ODBC], Access driver
- desktop database drivers [ODBC], Access driver
ms.assetid: 1690eb71-0cd3-4c00-9e15-f6a3ac5316dd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9ae798b3c3d91917e461bb6b5a58cb06734870d1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412421"
---
# <a name="setting-options-programmatically-for-the-access-driver"></a>Opciones de configuración mediante programación para el controlador de acceso

|Opción|Descripción|Método|  
|------------|-----------------|------------|  
|Tamaño del búfer|Tamaño del búfer interno, en kilobytes, que utiliza Microsoft Access para transferir datos hacia y desde el disco. El tamaño de búfer predeterminado es 2048 KB (se muestra como 2048). Se puede especificar cualquier valor entero divisible por 256.|Para establecer esta opción de forma dinámica, utilice la palabra clave MAXBUFFERSIZE en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Data Source Name|Nombre que identifica el origen de datos, como por ejemplo, nómina o personal.|Para establecer esta opción de forma dinámica, utilice la palabra clave **DSN** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Base de datos|Se puede configurar un origen de datos de Microsoft Access sin necesidad de seleccionar o crear una base de datos. Si no se proporciona ninguna base de datos al realizar la instalación, se le pedirá al usuario que elija un archivo de base de datos al conectarse al origen de datos.|Para establecer esta opción de forma dinámica, utilice la palabra clave **DBQ** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Descripción|Una descripción opcional de los datos del origen de datos; por ejemplo, "fecha de contratación, historial de salario y revisión actual de todos los empleados".|Para establecer esta opción de forma dinámica, utilice la palabra clave **Description** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Exclusivo|Si se selecciona el cuadro **exclusivo** , la base de datos se abrirá en modo exclusivo y solo un usuario podrá acceder a ella a la vez. El rendimiento se mejora cuando se ejecuta en modo exclusivo.|Para establecer esta opción de forma dinámica, utilice la palabra clave **Exclusive** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|ImplicitCommitSync|Determina cómo se escriben los cambios realizados fuera de una transacción en la base de datos. Este valor se establece inicialmente en "sí", lo que significa que el controlador de Microsoft Access esperará a que se completen las confirmaciones en una transacción interna/implícita.|Esta opción está incluida en el cuadro de diálogo **establecer opciones avanzadas** del controlador de Microsoft Access.|  
|Tiempo de espera de página|Especifica el período de tiempo, en milisegundos, que una página (si no se usa) permanece en el búfer antes de quitarse. En el caso del controlador de Microsoft Access, el valor predeterminado es 500 milisegundos (0,5 segundos). Esta opción se aplica a todos los orígenes de datos que utilizan el controlador ODBC.<br /><br /> El tiempo de espera de la página no puede ser 0 debido a un retraso inherente. El tiempo de espera de la página no puede ser menor que el retraso inherente, aunque la opción de tiempo de espera de la página esté establecida por debajo de ese valor.|Para establecer esta opción de forma dinámica, utilice la palabra clave **PAGETIMEOUT** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Solo lectura|Designa la base de datos como de solo lectura.|Para establecer esta opción de forma dinámica, utilice la palabra clave **ReadOnly** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Base de datos del sistema|La ruta de acceso completa de la base de datos del sistema de Microsoft Access que se va a usar con la base de datos de Microsoft Access a la que desea acceder.<br /><br /> Haga clic en el botón **base de datos del sistema** para seleccionar la base de datos del sistema que se va a usar. El controlador ODBC de Microsoft Access solicita al usuario un nombre y una contraseña. El nombre predeterminado es admin y la contraseña predeterminada en Microsoft Access para el usuario administrador es una cadena vacía.<br /><br /> Para aumentar la seguridad de la base de datos de Microsoft Access, cree un nuevo usuario para reemplazar al usuario administrador y elimine el usuario administrador, o bien cambie los objetos a los que tiene acceso el usuario administrador.|Para establecer esta opción de forma dinámica, utilice la palabra clave **SYSTEMDB** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Subprocesos|Número de subprocesos en segundo plano que va a usar el motor. En el caso del controlador de Microsoft Access, este valor tiene como valor predeterminado 3, pero se puede cambiar. Es posible que el usuario desee aumentar el número de subprocesos si hay una gran cantidad de actividad en la base de datos.<br /><br /> Esta opción está incluida en el cuadro de diálogo **establecer opciones avanzadas** del controlador de Microsoft Access.|Para establecer esta opción de forma dinámica, utilice la palabra clave **threads** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|UserCommitSync|Determina si el controlador de Microsoft Access realizará de forma asincrónica las transacciones explícitas definidas por el usuario. Este valor se establece inicialmente en "sí", lo que significa que el controlador de Microsoft Access esperará a que se completen las confirmaciones en una transacción definida por el usuario.<br /><br /> Establecer esta opción en false puede tener consecuencias imprevisibles en un entorno de varios usuarios.|Para establecer esta opción de forma dinámica, utilice la palabra clave **USERCOMMITSYNC** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|
