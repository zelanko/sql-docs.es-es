---
title: Solución de problemas (controlador ODBC de Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- set ANSI [ODBC]
- troubleshooting Visual FoxPro ODBC driver [ODBC]
- remote views [ODBC]
- multitiered views [ODBC]
- parameterized views [ODBC], Visual FoxPro ODBC driver
- fetches [ODBC], Visual FoxPro ODBC driver
- positioned updates [ODBC]
- background fetching [ODBC]
ms.assetid: fd478dd8-666a-4f0a-a2d6-b94e81cbbe4b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7f0576d017068b8ab0694da798c5be458f115e56
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47667973"
---
# <a name="troubleshooting-visual-foxpro-odbc-driver"></a>Solución de problemas (controlador ODBC de Visual FoxPro)
Las secciones siguientes describen cómo mejorar el rendimiento y resolver los problemas que pueden surgir al usar el controlador ODBC de Visual FoxPro.  
  
## <a name="accessing-parameterized-views"></a>Acceso a las vistas con parámetros  
 No se puede tener acceso a vistas con parámetros en una base de datos de Visual FoxPro con el controlador. Una vista con parámetros, crea una cláusula WHERE en SQL la vista **seleccione** instrucción que limita los registros se descarga en los registros que cumplen las condiciones de la cláusula WHERE creados con el valor proporcionado para el parámetro. Dado que el controlador no admite pasar parámetros a la vista, intenta obtener acceso a una vista con parámetros mediante el controlador generará un error.  
  
 El valor del parámetro puede ser proporcionado en tiempo de ejecución o pasar mediante programación a la vista.  
  
## <a name="accessing-remote-views"></a>Obtener acceso a vistas remotas  
 No se puede tener acceso a vistas remotas en una base de datos de Visual FoxPro con el controlador. Vistas remotas son vistas que tienen acceso a datos que no sean FoxPro o una combinación de FoxPro y datos que no sean FoxPro. Para obtener acceso a vistas remotas, use Visual FoxPro.  
  
## <a name="deleting-records"></a>Eliminación de registros  
 Puede marcar los registros para su eliminación con el controlador, pero definitivamente no se puede quitar los registros de la base de datos. Para quitar permanentemente los registros de una tabla, use Visual FoxPro.  
  
## <a name="increasing-performance-using-background-fetching"></a>Aumento del rendimiento mediante la recuperación en segundo plano  
 Puede mejorar el rendimiento en recuperaciones de gran tamaño mediante el uso de segundo plano capturando la característica del controlador. Recuperación en segundo plano usa un subproceso independiente para capturar los datos solicitados desde un origen de datos específico.  
  
 Puede emplear en segundo plano la obtención de un origen de datos en una de las maneras siguientes:  
  
-   Compruebe el **capturar los datos en segundo plano** casilla de verificación en la [cuadro de diálogo del programa de instalación de Visual FoxPro ODBC](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md).  
  
-   Use la palabra clave de atributo BackgroundFetch en la cadena de conexión.  
  
 Para obtener información sobre palabras clave de atributo de cadena de conexión, consulte [utilizando las cadenas de conexión](../../odbc/microsoft/using-connection-strings.md).  
  
## <a name="updating-multitiered-views"></a>Actualizar las vistas de varios niveles  
 Una vista de varios niveles es una vista basada en una o varias vistas en lugar de una tabla base. Al actualizar datos en una vista de varios niveles, las actualizaciones de bajar sólo un nivel a la vista en el que se basa la vista de nivel superior; no se actualizan las tablas base.  
  
## <a name="using-data-definition-language-ddl-in-stored-procedures"></a>Mediante el lenguaje de definición de datos (DDL) en los procedimientos almacenados  
 No se puede utilizar DDL como CREATE TABLE o ALTER TABLE en procedimientos almacenados de Visual FoxPro.  
  
 Para obtener información sobre el lenguaje que puede utilizar en los procedimientos almacenados, vea [compatibilidad con procedimientos almacenados, desencadenadores, valores predeterminados y reglas](../../odbc/microsoft/support-rules-triggers-defaults-stored-procedures-visual-foxpro-odbc-driver.md).  
  
## <a name="using-positioned-updates"></a>Uso de actualizaciones por posición  
 El controlador no es compatible con las actualizaciones posicionadas. Use la cláusula WHERE de SQL para identificar las filas que desea actualizar.  
  
## <a name="using-the-set-ansi-command"></a>Uso del comando de ANSI SET.  
 Si es un desarrollador de Visual FoxPro, debe tener en cuenta que el valor predeterminado de SET ANSI está activado para el controlador, a diferencia de un valor predeterminado desactivado para Visual FoxPro. El valor predeterminado en la configuración de SET ANSI permite que los orígenes de datos de Visual FoxPro a comportarse de forma coherente con otros orígenes de datos ODBC que suelen realizan comparaciones exactas. Puede cambiar la configuración predeterminada. Para obtener más información, consulte [SET ANSI](../../odbc/microsoft/set-ansi-command.md).
