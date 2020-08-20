---
description: Solución de problemas (controlador ODBC de Visual FoxPro)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 73f98f66a09b0ff17987186103b38643047f1762
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471438"
---
# <a name="troubleshooting-visual-foxpro-odbc-driver"></a>Solución de problemas (controlador ODBC de Visual FoxPro)
En las secciones siguientes se explica cómo mejorar el rendimiento y resolver los problemas que pueden surgir al usar el controlador ODBC de Visual FoxPro.  
  
## <a name="accessing-parameterized-views"></a>Obtener acceso a vistas con parámetros  
 No se puede tener acceso a las vistas con parámetros en una base de datos de Visual FoxPro mediante el controlador. Una vista con parámetros crea una cláusula WHERE en la instrucción **Select** de SQL de la vista que limita los registros descargados a los registros que cumplen las condiciones de la cláusula WHERE compilada con el valor proporcionado para el parámetro. Dado que el controlador no permite pasar parámetros a la vista, se producirá un error al intentar obtener acceso a una vista con parámetros mediante el controlador.  
  
 El valor del parámetro se puede proporcionar en tiempo de ejecución o pasar mediante programación a la vista.  
  
## <a name="accessing-remote-views"></a>Acceder a vistas remotas  
 No se puede tener acceso a las vistas remotas en una base de datos de Visual FoxPro mediante el controlador. Las vistas remotas son vistas que tienen acceso a datos que no son de FoxPro o a una combinación de datos de FoxPro y que no son de FoxPro. Para tener acceso a las vistas remotas, utilice Visual FoxPro.  
  
## <a name="deleting-records"></a>Eliminar registros  
 Puede marcar los registros para su eliminación mediante el controlador, pero no puede quitar los registros de la base de datos de forma permanente. Para quitar permanentemente los registros de una tabla, utilice Visual FoxPro.  
  
## <a name="increasing-performance-using-background-fetching"></a>Aumento del rendimiento mediante la captura en segundo plano  
 Puede mejorar el rendimiento en capturas grandes mediante la característica de captura en segundo plano del controlador. La captura en segundo plano usa un subproceso independiente para capturar los datos solicitados de un origen de datos concreto.  
  
 Puede usar la captura en segundo plano para un origen de datos de una de las siguientes maneras:  
  
-   Active la casilla **recuperar datos en segundo plano** en el [cuadro de diálogo Configuración de ODBC Visual FoxPro](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md).  
  
-   Use la palabra clave del atributo BackgroundFetch en la cadena de conexión.  
  
 Para obtener información sobre las palabras clave de atributo de cadena de conexión, vea [usar cadenas de conexión](../../odbc/microsoft/using-connection-strings.md).  
  
## <a name="updating-multitiered-views"></a>Actualizar vistas de varios niveles  
 Una vista multinivel es una vista basada en una o varias vistas en lugar de en una tabla base. Cuando se actualizan datos en una vista de varios niveles, las actualizaciones se desactivan en un solo nivel hasta la vista en la que se basa la vista de nivel superior. las tablas base no se actualizan.  
  
## <a name="using-data-definition-language-ddl-in-stored-procedures"></a>Usar el lenguaje de definición de datos (DDL) en procedimientos almacenados  
 No se puede usar DDL, como CREATE TABLE o ALTER TABLE, en procedimientos almacenados de Visual FoxPro.  
  
 Para obtener información sobre el lenguaje que se puede usar en procedimientos almacenados, vea [compatibilidad con reglas, desencadenadores, valores predeterminados y procedimientos almacenados](../../odbc/microsoft/support-rules-triggers-defaults-stored-procedures-visual-foxpro-odbc-driver.md).  
  
## <a name="using-positioned-updates"></a>Usar actualizaciones posicionadas  
 El controlador no admite actualizaciones posicionadas. Utilice la cláusula WHERE de SQL para identificar las filas que desea actualizar.  
  
## <a name="using-the-set-ansi-command"></a>Usar el comando SET ANSI  
 Si es desarrollador de Visual FoxPro, debe tener en cuenta que la configuración predeterminada de SET ANSI está activada para el controlador, a diferencia de la configuración predeterminada de OFF para Visual FoxPro. El valor predeterminado al establecer para SET ANSI permite que los orígenes de datos de Visual FoxPro se comporten de forma coherente con otros orígenes de datos ODBC que normalmente realizan comparaciones exactas. Puede cambiar la configuración predeterminada. Para obtener más información, vea [set ANSI](../../odbc/microsoft/set-ansi-command.md).
