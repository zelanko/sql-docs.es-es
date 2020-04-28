---
title: Formato de cadena de conexión y atributos | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81281155"
---
# <a name="connection-string-format-and-attributes"></a>Atributos y el formato de cadena de conexión
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 En lugar de usar un cuadro de diálogo, algunas aplicaciones pueden requerir una cadena de conexión que especifique la información de conexión a un origen de datos. La cadena de conexión se compone de una serie de atributos que especifican cómo se conecta un controlador a un origen de datos. Un atributo identifica una parte específica de la información que el controlador debe conocer antes de poder crear la conexión de origen de datos adecuada. Cada controlador puede tener un conjunto diferente de atributos, pero el formato de la cadena de conexión siempre es el mismo. Una cadena de conexión tiene el formato siguiente:  
  
```  
"DSN=data-source-name[;SERVER=value] [;PWD=value] [;UID=value] [;<Attribute>=<value>]"  
```  
  
> [!NOTE]  
>  Microsoft ODBC driver for Oracle admite el formato de cadena de conexión de la primera versión del controlador, que usa `CONNECTSTRING`= en lugar de `SERVER=`.  
  
 Si se va a conectar a un proveedor de origen de datos que admite la autenticación de `Trusted_Connection=yes` Windows, debe especificar en lugar de la información de ID. de usuario y contraseña en la cadena de conexión.  
  
 Debe especificar el nombre del origen de datos si no especifica los atributos UID, PWD, SERVER (o CONNECTSTRING) y DRIVER. Sin embargo, todos los demás atributos son opcionales. Si no especifica ningún atributo, ese atributo tiene como valor predeterminado el que se especifica en la ficha DSN correspondiente del cuadro de diálogo **Administrador de orígenes de datos ODBC** . El valor del atributo puede distinguir entre mayúsculas y minúsculas.  
  
 Los atributos de la cadena de conexión son los siguientes:  
  
|Atributo|Descripción|Valor predeterminado|  
|---------------|-----------------|-------------------|  
|DSN|El nombre del origen de datos que aparece en la ficha Controladores del cuadro de diálogo **Administrador de orígenes de datos ODBC** .|""|  
|PWD|La contraseña del servidor de Oracle al que desea obtener acceso. Este controlador es compatible con las limitaciones que Oracle coloca en las contraseñas.|""|  
|SERVER|Cadena de conexión para el servidor de Oracle al que desea obtener acceso.|""|  
|UID|El nombre de usuario del servidor de Oracle. Dependiendo del sistema, este atributo podría no ser opcional, es decir, algunas bases de datos y tablas podrían requerir este atributo por motivos de seguridad.<br /><br /> Use "/" para usar la autenticación de sistema operativo de Oracle.|""|  
|BUFFERSIZE|Tamaño de búfer óptimo que se usa al capturar columnas.<br /><br /> El controlador optimiza la captura para que una captura del servidor de Oracle devuelva suficientes filas para rellenar un búfer de este tamaño. Los valores más grandes tienden a aumentar el rendimiento si se capturan muchos datos.|65535|  
|SYNONYMCOLUMNS|Cuando este valor es true (1), una llamada a la API SQLColumn () devuelve información de columna. De lo contrario, SQLColumn () solo devuelve las columnas de las tablas y vistas. El controlador ODBC para Oracle proporciona un acceso más rápido cuando no se establece este valor.|1|  
|COMENTARIOS|Cuando este valor es true (1), el controlador devuelve las columnas de comentarios para el conjunto de resultados [SQLColumns](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md) . El controlador ODBC para Oracle proporciona un acceso más rápido cuando no se establece este valor.|0|  
|StdDayOfWeek|Aplica el estándar ODBC para el escalar DAYOFWEEK. De forma predeterminada, esta opción está activada, pero los usuarios que necesitan la versión localizada pueden cambiar el comportamiento para usar lo que devuelva Oracle.|1|  
|GuessTheColDef|Especifica si el controlador debe devolver o no un valor distinto de cero para el argumento *cbColDef* de **SQLDescribeCol**. Solo se aplica a las columnas en las que no hay ninguna escala definida por Oracle, como columnas numéricas calculadas y columnas definidas como número sin una precisión o escala. Una llamada a **SQLDescribeCol** devuelve 130 para la precisión cuando Oracle no proporciona esa información.|0|  
  
 Por ejemplo, una cadena de conexión que se conecta al origen de datos de mi DataSource mediante el servidor MyOracleServerOracle y el usuario de Oracle suuserid sería:  
  
```  
"DSN={MyDataSource};UID={MyUserID};PWD={MyPassword};SERVER={MyOracleServer}"  
```  
  
 Una cadena de conexión que se conecta al origen de datos MyOtherDataSource mediante la autenticación del sistema operativo y el servidor MyOtherOracleServerOracle sería:  
  
```  
"DSN=MyOtherDataSource;UID=/;PWD=;SERVER=MyOtherOracleServer"  
```
