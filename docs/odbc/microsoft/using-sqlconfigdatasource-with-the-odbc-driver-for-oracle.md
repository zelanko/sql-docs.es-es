---
title: Utilizando SQLConfigDatasource con el controlador ODBC para Oracle | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], ODBC driver for Oracle
ms.assetid: e535d1ef-aff9-4ae7-a3ed-ef4ca2584289
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fa5f1ecf9f3100480081e3744fc7d280a4da282b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088030"
---
# <a name="using-sqlconfigdatasource-with-the-odbc-driver-for-oracle"></a>Utilizando SQLConfigDatasource con el controlador ODBC para Oracle
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, use el controlador ODBC proporcionado por Oracle.  
  
 La siguiente tabla enumera válido **SQLConfigDatasource** configuración para el controlador ODBC de Microsoft para Oracle, versión 1.0 (Msorcl10.dll) y el controlador ODBC de Microsoft para Oracle, versión 2.0 (Sqlsrv32).  
  
> [!NOTE]  
>  El controlador Msorcl10.dll (versión 1.0) es compatible con todas las configuraciones excepto **Server**. El controlador Sqlsrv32 (versión 2.0 y versiones posterior) es compatible con todas las configuraciones.  
  
 Algunas opciones de configuración se omiten el controlador, pero acepta **SQLConfigDatasource**. Incluir esta configuración en la cadena de conexión de ODBC es la única manera que se aceptarán en tiempo de ejecución. No se almacenarán en el registro de una configuración omitida cuando **SQLConfigDatasource** crea el origen de datos.  
  
 En la tabla siguiente, *A/N* significa cualquier cadena alfanumérica válida hasta la longitud máxima permitida. *Max Len* (longitud máxima) es la longitud máxima de la cadena aceptada por la configuración, incluido el carácter del terminador de cadena.  
  
|Parámetro|Longitud máxima|Valor predeterminado|Valores válidos|Descripción|  
|-------------|-------------|-------------------|------------------|-----------------|  
|BufferSize|7|65535|1000|Un máximo de 65535 bytes de tamaño de búfer de captura mínimo|  
|CatalogCap|2|1|0 o 1|Si es 1, los identificadores nonquoted será funciones convertidas a mayúsculas en el catálogo.|  
|ConnectString|128|""|A/N|Cadena de conexión Método necesario para especificar el nombre del servidor con el controlador Msorcl10.dll.|  
|Descripción|256|""|A/N|Descripción.|  
|DSN|33|""|A/N|Nombre del origen de datos.|  
|GuessTheColDef|4|0|A/N|Devuelve un valor distinto de cero para las columnas sin escala definido por Oracle.|  
|NumberFloat|2|""|0 o 1|Si es 0, las columnas de tipo FLOAT se tratan como SQL_FLOAT. Si es 1, FLOAT columnas se tratan como SQL_DOUBLE.|  
|PWD|30|""|A/N|Contraseña.|  
|RDOSupport|2|""|0 o 1|Permite RDO llamar a procedimientos de Oracle.|  
|Comentarios|2|0|0 o 1|Incluir comentarios en las funciones de catálogo.|  
|RowLimit|4|""|0 y 99|Número máximo de filas devueltas por una instrucción SELECT. Una cadena de longitud cero indica que no se aplica ningún límite.|  
|Server|128|""|A/N|Nombre del servidor de Oracle.|  
|SynonymColumns|2|1|0 o 1|Incluir sinónimos en SQLColumns.|  
|SystemTable|2|""|0 o 1|Si es 0, no se mostrarán las tablas del sistema. Si es 1, se mostrará en las tablas del sistema.|  
|TranslationDLL|33|""|A/N|Nombre de la DLL de traducción.|  
|TranslationName|33|""|A/N|Nombre de la traducción.|  
|TranslationOption|33|""|A/N|Opción de traducción.|  
|TxnCap|2|""|A/N|Compatible con la transacción. Si es 0, el controlador informa de que no es compatible con las transacciones. Si es 1, el controlador informa que es capaz de realizar las transacciones.|  
|UID|30|""|A/N|Nombre de usuario.|
