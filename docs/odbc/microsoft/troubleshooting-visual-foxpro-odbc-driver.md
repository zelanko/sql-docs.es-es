---
title: Solución de problemas (controlador ODBC de Visual FoxPro) | Documentos de Microsoft
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
ms.topic: article
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
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 95a7ca8185fba077966caba1715b2359f73c4336
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="troubleshooting-visual-foxpro-odbc-driver"></a>Solución de problemas (controlador ODBC de Visual FoxPro)
Las secciones siguientes describen cómo mejorar el rendimiento y resolver los problemas que podrían surgir al usar el controlador ODBC de Visual FoxPro.  
  
## <a name="accessing-parameterized-views"></a>Obtener acceso a vistas con parámetros  
 No se puede tener acceso a vistas con parámetros en una base de datos de Visual FoxPro con el controlador. Una vista con parámetros crea una cláusula WHERE en SQL la vista **seleccione** instrucción que limita los registros que se descarga en los registros que cumplen las condiciones de la cláusula WHERE que se generan con el valor proporcionado para el parámetro. Dado que el controlador no admite pasar parámetros a la vista, se producirá un error intenta obtener acceso a una vista con parámetros mediante el controlador.  
  
 El valor del parámetro puede ser proporcionado en tiempo de ejecución o pasar mediante programación a la vista.  
  
## <a name="accessing-remote-views"></a>Obtener acceso a vistas remotas  
 No se puede tener acceso a vistas remotas en una base de datos de Visual FoxPro con el controlador. Vistas remotas son vistas que tienen acceso a datos no FoxPro o una combinación de FoxPro y FoxPro no datos. Para obtener acceso a vistas remotas, use Visual FoxPro.  
  
## <a name="deleting-records"></a>Eliminación de registros  
 Puede marcar los registros para su eliminación con el controlador, pero no se puede quitar permanentemente los registros de la base de datos. Para quitar permanentemente los registros de una tabla, use Visual FoxPro.  
  
## <a name="increasing-performance-using-background-fetching"></a>Aumento del rendimiento mediante la recuperación en segundo plano  
 Puede mejorar el rendimiento en capturas grandes utilizando el fondo obtener características del controlador. Recuperación en segundo plano usa un subproceso independiente para capturar los datos solicitados desde un origen de datos específico.  
  
 Puede emplear el fondo de filas para un origen de datos en una de las maneras siguientes:  
  
-   Compruebe el **capturar los datos en segundo plano** casilla de verificación en la [cuadro de diálogo del programa de instalación de Visual FoxPro ODBC](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md).  
  
-   Utilice la palabra clave de atributo de BackgroundFetch en la cadena de conexión.  
  
 Para obtener información sobre palabras clave de atributo de cadena de conexión, consulte [uso de cadenas de conexión](../../odbc/microsoft/using-connection-strings.md).  
  
## <a name="updating-multitiered-views"></a>Actualizar las vistas de varias capas  
 Una vista de varias capas es una vista basada en una o varias vistas, en lugar de en una tabla base. Al actualizar datos en una vista de varias capas, las actualizaciones de bajar de un solo nivel, a la vista en la que se basa la vista de nivel superior; no se actualizan las tablas base.  
  
## <a name="using-data-definition-language-ddl-in-stored-procedures"></a>Con el lenguaje de definición de datos (DDL) en los procedimientos almacenados  
 No se puede utilizar DDL, como CREATE TABLE o ALTER TABLE, en los procedimientos almacenados de Visual FoxPro.  
  
 Para obtener información sobre el lenguaje que se puede usar en los procedimientos almacenados, vea [compatibilidad con procedimientos almacenados, desencadenadores, valores predeterminados y reglas](../../odbc/microsoft/support-rules-triggers-defaults-stored-procedures-visual-foxpro-odbc-driver.md).  
  
## <a name="using-positioned-updates"></a>Uso de actualizaciones por posición  
 El controlador no es compatible con actualizaciones por posición. Utilice la cláusula WHERE de SQL para identificar las filas que desea actualizar.  
  
## <a name="using-the-set-ansi-command"></a>Utiliza el comando de ANSI SET.  
 Si es un desarrollador de Visual FoxPro, debe tener en cuenta que el valor predeterminado de SET ANSI está activado para el controlador, a diferencia de un valor predeterminado de OFF de Visual FoxPro. El valor predeterminado en la configuración de SET ANSI permite orígenes de datos de Visual FoxPro para comportarse de forma coherente con otros orígenes de datos ODBC que normalmente se realizan las comparaciones exactas. Puede cambiar la configuración predeterminada. Para obtener más información, consulte [SET ANSI](../../odbc/microsoft/set-ansi-command.md).
