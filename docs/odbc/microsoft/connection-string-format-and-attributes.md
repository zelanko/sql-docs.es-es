---
title: Formato y atributos de la cadena de conexión ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection strings [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], connection strings
ms.assetid: 0c360112-8720-4e54-a1a6-b9b18d943557
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d95866976d2e83c058f83b3a0ae5e9a4e8888ed1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81281155"
---
# <a name="connection-string-format-and-attributes"></a>Atributos y el formato de cadena de conexión
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 En lugar de usar un cuadro de diálogo, algunas aplicaciones pueden requerir una cadena de conexión que especifique la información de conexión del origen de datos. La cadena de conexión se compone de una serie de atributos que especifican cómo se conecta un controlador a un origen de datos. Un atributo identifica una información específica que el controlador necesita saber antes de que pueda realizar la conexión de origen de datos adecuada. Cada controlador puede tener un conjunto diferente de atributos, pero el formato de cadena de conexión siempre es el mismo. Una cadena de conexión tiene el siguiente formato:  
  
```  
"DSN=data-source-name[;SERVER=value] [;PWD=value] [;UID=value] [;<Attribute>=<value>]"  
```  
  
> [!NOTE]  
>  El controlador ODBC de Microsoft para Oracle admite el formato de `CONNECTSTRING`cadena `SERVER=`de conexión de la primera versión del controlador, que utilizaba .  
  
 Si se conecta a un proveedor de origen de `Trusted_Connection=yes` datos que admite la autenticación de Windows, debe especificar en lugar de la información de ID de usuario y contraseña en la cadena de conexión.  
  
 Debe especificar el nombre del origen de datos si no especifica los atributos UID, PWD, SERVER (o CONNECTSTRING) y DRIVER. Sin embargo, todos los demás atributos son opcionales. Si no especifica un atributo, ese atributo tiene como valor predeterminado el especificado en la ficha DSN correspondiente del cuadro de diálogo **Administrador de orígenes** de datos ODBC. El valor del atributo puede distinguir entre mayúsculas y minúsculas.  
  
 Los atributos de la cadena de conexión son los siguientes:  
  
|Atributo|Descripción|Valor predeterminado|  
|---------------|-----------------|-------------------|  
|DSN|El nombre del origen de datos que aparece en la pestaña Controladores del cuadro de diálogo **Administrador de orígenes** de datos ODBC.|""|  
|PWD|La contraseña del servidor de Oracle al que desea acceder. Este controlador admite las limitaciones que Oracle coloca en las contraseñas.|""|  
|SERVER|La cadena de conexión para el servidor de Oracle al que desea tener acceso.|""|  
|UID|El nombre de usuario de Oracle Server. Dependiendo del sistema, este atributo podría no ser opcional, es decir, ciertas bases de datos y tablas pueden requerir este atributo por motivos de seguridad.<br /><br /> Utilice "/" para utilizar la autenticación del sistema operativo de Oracle.|""|  
|BUFFERSIZE|El tamaño de búfer óptimo utilizado al capturar columnas.<br /><br /> El controlador optimiza la obtención para que una captura del servidor de Oracle devuelva suficientes filas para rellenar un búfer de este tamaño. Los valores más grandes tienden a aumentar el rendimiento si se capturan una gran cantidad de datos.|65535|  
|SYNONYMCOLUMNS|Cuando este valor es true (1), una llamada a la API SQLColumn( ) devuelve información de columna. De lo contrario, SQLColumn( ) devuelve solo columnas para tablas y vistas. El controlador ODBC para Oracle proporciona un acceso más rápido cuando no se establece este valor.|1|  
|COMENTARIOS|Cuando este valor es true (1), el controlador devuelve columnas Remarks para el conjunto de resultados [SQLColumns.](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md) El controlador ODBC para Oracle proporciona un acceso más rápido cuando no se establece este valor.|0|  
|StdDayOfWeek|Aplica el estándar ODBC para el escalar DAYOFWEEK. De forma predeterminada, está activado, pero los usuarios que necesitan la versión localizada pueden cambiar el comportamiento para usar lo que Oracle devuelva.|1|  
|GuessTheColDef|Especifica si el controlador debe devolver o no un valor distinto de cero para el *argumento cbColDef* de **SQLDescribeCol**. Solo se aplica a las columnas en las que no hay ninguna escala definida por Oracle, como columnas numéricas calculadas y columnas definidas como NUMBER sin precisión ni escala. Una llamada **SQLDescribeCol** devuelve 130 para la precisión cuando Oracle no proporciona esa información.|0|  
  
 Por ejemplo, una cadena de conexión que se conecta al origen de datos MyDataSource mediante MyOracleServerOracle Server y Oracle User MyUserID sería:  
  
```  
"DSN={MyDataSource};UID={MyUserID};PWD={MyPassword};SERVER={MyOracleServer}"  
```  
  
 Una cadena de conexión que se conecta al origen de datos MyOtherDataSource mediante la autenticación del sistema operativo y el servidor MyOtherOracleServerOracle sería:  
  
```  
"DSN=MyOtherDataSource;UID=/;PWD=;SERVER=MyOtherOracleServer"  
```
