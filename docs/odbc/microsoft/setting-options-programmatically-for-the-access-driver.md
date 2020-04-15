---
title: Configuración de opciones mediante programación para el controlador de acceso ? Microsoft Docs
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
ms.openlocfilehash: 9a90f0a20569a2a0a5bb93dec7aa4b95b50093dc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300795"
---
# <a name="setting-options-programmatically-for-the-access-driver"></a>Opciones de configuración mediante programación para el controlador de acceso

|Opción|Descripción|Método|  
|------------|-----------------|------------|  
|Tamaño del búfer|El tamaño del búfer interno, en kilobytes, que utiliza Microsoft Access para transferir datos desde y hacia el disco. El tamaño de búfer predeterminado es 2048 KB (se muestra como 2048). Se puede introducir cualquier valor entero divisible por 256.|Para establecer esta opción dinámicamente, utilice la palabra clave MAXBUFFERSIZE en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Data Source Name|Nombre que identifica el origen de datos, como Cálculo de nómina o Personal.|Para establecer esta opción dinámicamente, utilice la palabra clave **DSN** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Base de datos|Un origen de datos de Microsoft Access se puede configurar sin seleccionar ni crear una base de datos. Si no se proporciona ninguna base de datos al configurarla, se pedirá al usuario que elija un archivo de base de datos al conectarse al origen de datos.|Para establecer esta opción dinámicamente, utilice la palabra clave **DBQ** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Descripción|Una descripción opcional de los datos en el origen de datos; por ejemplo, "Fecha de contratación, historial salarial y revisión actual de todos los empleados".|Para establecer esta opción dinámicamente, utilice la palabra clave **DESCRIPTION** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Exclusivo|Si se selecciona el cuadro **Exclusivo,** la base de datos se abrirá en modo Exclusivo y solo un usuario podrá acceder a ella. El rendimiento se mejora cuando se ejecuta en modo exclusivo.|Para establecer esta opción dinámicamente, utilice la palabra clave **EXCLUSIVE** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|ImplicitCommitSync|Determina cómo se escriben en la base de datos los cambios realizados fuera de una transacción. Este valor se establece inicialmente en "Sí", lo que significa que el controlador de Microsoft Access esperará a que se completen las confirmaciones en una transacción interna/implícita.|Esta opción se incluye en el cuadro de diálogo **Establecer opciones avanzadas** para el controlador de Microsoft Access.|  
|Tiempo de espera de página|Especifica el período de tiempo, en milisegundos, que una página (si no se utiliza) permanece en el búfer antes de quitarse. Para el controlador de Microsoft Access, el valor predeterminado es 500 milisegundos (0,5 segundos). Esta opción se aplica a todos los orígenes de datos que usan el controlador ODBC.<br /><br /> El tiempo de espera de página no puede ser 0 debido a un retraso inherente. El tiempo de espera de página no puede ser menor que el retardo inherente, incluso si la opción de tiempo de espera de página se establece por debajo de ese valor.|Para establecer esta opción dinámicamente, utilice la palabra clave **PAGETIMEOUT** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Solo lectura|Designa la base de datos como de solo lectura.|Para establecer esta opción dinámicamente, utilice la palabra clave **READONLY** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Base de datos del sistema|La ruta de acceso completa de la base de datos del sistema de Microsoft Access que se usará con la base de datos de Microsoft Access a la que desea tener acceso.<br /><br /> Haga clic en el botón **Base de datos del** sistema para seleccionar la base de datos del sistema que se va a utilizar. El controlador ODBC de Microsoft Access solicita al usuario un nombre y una contraseña. El nombre predeterminado es Admin y la contraseña predeterminada en Microsoft Access para el usuario Admin es una cadena vacía.<br /><br /> Para aumentar la seguridad de la base de datos de Microsoft Access, cree un nuevo usuario para reemplazar al usuario administrador y elimine el usuario administrador, o cambie los objetos a los que tiene acceso el usuario administrador.|Para establecer esta opción dinámicamente, utilice la palabra clave **SYSTEMDB** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Subprocesos|El número de subprocesos en segundo plano que va a utilizar el motor. Para el controlador de Microsoft Access, este valor predeterminado es 3, pero se puede cambiar. Es posible que el usuario desee aumentar el número de subprocesos si hay una gran cantidad de actividad en la base de datos.<br /><br /> Esta opción se incluye en el cuadro de diálogo **Establecer opciones avanzadas** para el controlador de Microsoft Access.|Para establecer esta opción dinámicamente, utilice la palabra clave **THREADS** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|UserCommitSync|Determina si el controlador de Microsoft Access realizará una transacción explícita definida por el usuario de forma asincrónica. Este valor se establece inicialmente en "Sí", lo que significa que el controlador de Microsoft Access esperará a que se completen las confirmaciones en una transacción definida por el usuario.<br /><br /> Establecer esta opción en False puede tener consecuencias impredecibles en un entorno multiusuario.|Para establecer esta opción dinámicamente, utilice la palabra clave **USERCOMMITSYNC** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|
