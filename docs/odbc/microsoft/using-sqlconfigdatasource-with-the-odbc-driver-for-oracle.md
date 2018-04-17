---
title: Utilizando SQLConfigDatasource con el controlador ODBC para Oracle | Documentos de Microsoft
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
- SQLConfigDataSource function [ODBC], ODBC driver for Oracle
ms.assetid: e535d1ef-aff9-4ae7-a3ed-ef4ca2584289
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6042e30479c21437885388579325b22c5de381fb
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="using-sqlconfigdatasource-with-the-odbc-driver-for-oracle"></a>Utilizando SQLConfigDatasource con el controlador ODBC para Oracle
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 La siguiente tabla se recogen válido **SQLConfigDatasource** configuración para el controlador ODBC de Microsoft para Oracle, versión 1.0 (Msorcl10.dll) y el controlador ODBC de Microsoft para Oracle, versión 2.0 (Sqlsrv32).  
  
> [!NOTE]  
>  El controlador de Msorcl10.dll (versión 1.0) admite todos los valores excepto **Server**. El controlador de Sqlsrv32 (versión 2.0 y versiones posterior) es compatible con todas las configuraciones.  
  
 Algunas opciones de configuración se omiten el controlador, pero acepta **SQLConfigDatasource**. Incluir esta configuración en la cadena de conexión de ODBC es la única manera de que se aceptarán en tiempo de ejecución. Un valor omitido no se almacenarán en el registro cuando **SQLConfigDatasource** crea el origen de datos.  
  
 En la siguiente tabla, *A/N* significa cualquier cadena alfanumérica válido hasta la longitud máxima permitida. *Max Len* (longitud máxima) es la longitud máxima permitida de la cadena aceptada la configuración, incluido el carácter de terminador de cadena.  
  
|Configuración|Longitud máxima|Valor predeterminado|Valores válidos|Description|  
|-------------|-------------|-------------------|------------------|-----------------|  
|BufferSize|7|65535|1000|Un máximo de 65535 bytes de tamaño de búfer de captura mínima|  
|CatalogCap|2|1|0 o 1|Si es 1, identificadores nonquoted será funciones convierte a mayúsculas en el catálogo.|  
|ConnectString|128|""|A/N|Cadena de conexión Método necesario para especificar el nombre del servidor con el controlador Msorcl10.dll.|  
|Description|256|""|A/N|Descripción.|  
|DSN|33|""|A/N|Nombre de origen de datos.|  
|GuessTheColDef|4|0|A/N|Devuelve un valor distinto de cero para las columnas sin escala definida por Oracle.|  
|NumberFloat|2|""|0 o 1|Si es 0, las columnas de tipo FLOAT se tratan como SQL_FLOAT. Si es 1, se consideran SQL_DOUBLE en columnas de tipo FLOAT.|  
|PWD|30|""|A/N|Contraseña.|  
|RDOSupport|2|""|0 o 1|Permite RDO llamar a procedimientos de Oracle.|  
|Comentarios|2|0|0 o 1|Incluir comentarios en funciones de catálogo.|  
|RowLimit|4|""|0 a 99|Número máximo de filas devueltas por una instrucción SELECT. Una cadena de longitud cero indica que no se aplica ningún límite.|  
|Server|128|""|A/N|Nombre de servidor de Oracle.|  
|SynonymColumns|2|1|0 o 1|Incluir SYNONYMs en SQLColumns.|  
|SystemTable|2|""|0 o 1|Si es 0, no se mostrarán las tablas del sistema. Si es 1, se mostrará en las tablas del sistema.|  
|TranslationDLL|33|""|A/N|Nombre de archivo .dll de traducción.|  
|TranslationName|33|""|A/N|Nombre de la traducción.|  
|TranslationOption|33|""|A/N|Opción de traducción.|  
|TxnCap|2|""|A/N|Compatible con la transacción. Si es 0, el controlador indica que no admite transacciones. Si es 1, el controlador indica que es capaz de llevar a cabo las transacciones.|  
|UID|30|""|A/N|Nombre de usuario.|
