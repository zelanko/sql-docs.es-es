---
title: Solución de problemas (controlador ODBC de Visual FoxPro) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 70b035069c0be88d05a3aa5e17b96af991c27405
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303036"
---
# <a name="troubleshooting-visual-foxpro-odbc-driver"></a>Solución de problemas (controlador ODBC de Visual FoxPro)
En las secciones siguientes se explica cómo mejorar el rendimiento y resolver los problemas que puede encontrar al usar el controlador ODBC de Visual FoxPro.  
  
## <a name="accessing-parameterized-views"></a>Acceso a vistas parametrizadas  
 No puede tener acceso a vistas parametrizadas en una base de datos de Visual FoxPro mediante el controlador. Una vista parametrizada crea una cláusula WHERE en la instrucción **SELECT** de SQL de la vista que limita los registros descargados a los registros que cumplen las condiciones de la cláusula WHERE creada con el valor proporcionado para el parámetro. Dado que el controlador no admite el paso de parámetros a la vista, se producirá un error al intentar acceder a una vista parametrizada mediante el controlador.  
  
 El valor del parámetro se puede proporcionar en tiempo de ejecución o pasar mediante programación a la vista.  
  
## <a name="accessing-remote-views"></a>Acceso a vistas remotas  
 No puede tener acceso a vistas remotas en una base de datos de Visual FoxPro mediante el controlador. Las vistas remotas son vistas que acceden a datos que no son de FoxPro o a una combinación de datos de FoxPro y no FoxPro. Para acceder a vistas remotas, utilice Visual FoxPro.  
  
## <a name="deleting-records"></a>Eliminación de registros  
 Puede marcar los registros para su eliminación mediante el controlador, pero no puede quitar permanentemente los registros de la base de datos. Para quitar registros de forma permanente de una tabla, utilice Visual FoxPro.  
  
## <a name="increasing-performance-using-background-fetching"></a>Aumento del rendimiento mediante la obtención en segundo plano  
 Puede mejorar el rendimiento en capturas grandes mediante la característica de obtención en segundo plano del controlador. La obtención en segundo plano utiliza un subproceso independiente para capturar los datos solicitados de un origen de datos específico.  
  
 Puede emplear la obtención en segundo plano para un origen de datos de una de las siguientes maneras:  
  
-   Marque la casilla de verificación **Obtener datos en segundo plano** en el cuadro de diálogo Configuración de ODBC Visual [FoxPro](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md).  
  
-   Utilice la palabra clave de atributo BackgroundFetch en la cadena de conexión.  
  
 Para obtener información sobre las palabras clave de atributo de cadena de conexión, consulte Uso de [cadenas](../../odbc/microsoft/using-connection-strings.md)de conexión .  
  
## <a name="updating-multitiered-views"></a>Actualización de vistas multinivel  
 Una vista de varios niveles es una vista basada en una o varias vistas en lugar de en una tabla base. Al actualizar datos en una vista de varios niveles, las actualizaciones van a bajar solo un nivel, a la vista en la que se basa la vista de nivel superior; las tablas base no se actualizan.  
  
## <a name="using-data-definition-language-ddl-in-stored-procedures"></a>Uso del lenguaje de definición de datos (DDL) en procedimientos almacenados  
 No puede usar DDL, como CREATE TABLE o ALTER TABLE, en procedimientos almacenados de Visual FoxPro.  
  
 Para obtener información sobre el lenguaje que puede usar en procedimientos almacenados, vea [Compatibilidad con reglas, desencadenadores, valores predeterminados y procedimientos almacenados](../../odbc/microsoft/support-rules-triggers-defaults-stored-procedures-visual-foxpro-odbc-driver.md).  
  
## <a name="using-positioned-updates"></a>Uso de actualizaciones posicionadas  
 El controlador no admite actualizaciones posicionadas. Utilice la cláusula WHERE de SQL para identificar las filas que desea actualizar.  
  
## <a name="using-the-set-ansi-command"></a>Uso del comando SET ANSI  
 Si es un desarrollador de Visual FoxPro, debe tener en cuenta que la configuración predeterminada de SET ANSI es ON para el controlador, a diferencia de un valor predeterminado de OFF para Visual FoxPro. La configuración ON predeterminada para SET ANSI permite que los orígenes de datos de Visual FoxPro se comporten de forma coherente con otros orígenes de datos ODBC que normalmente realizan comparaciones exactas. Puede cambiar la configuración predeterminada. Para obtener más información, consulte [SET ANSI](../../odbc/microsoft/set-ansi-command.md).
