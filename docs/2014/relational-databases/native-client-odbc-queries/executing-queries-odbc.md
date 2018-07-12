---
title: Ejecutar consultas (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ODBC applications, executing queries
- SQL Server Native Client ODBC driver, statements
- ODBC applications, statements
- SQL Server Native Client ODBC driver, queries
- queries [ODBC]
ms.assetid: d935bcba-8ce6-4159-8395-6c86431602ad
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 552a9d37d06ba145e371650dd56027ca38eb7c20
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37416284"
---
# <a name="executing-queries-odbc"></a>Ejecutar consultas (ODBC)
  Después de que una aplicación ODBC inicializa un identificador de conexión y conecta con un origen de datos, asigna uno o más identificadores de instrucciones en el identificador de conexión. A continuación, puede ejecutar la aplicación [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instrucciones en el identificador de instrucción. La secuencia general de eventos para ejecutar una instrucción SQL es:  
  
1.  Establezca los atributos de instrucción necesarios.  
  
2.  Construya la instrucción.  
  
3.  Ejecute la instrucción.  
  
4.  Recupere los conjuntos de resultados.  
  
 Después de que una aplicación recupera todas las filas en todos los conjuntos de resultados devueltos por la instrucción SQL, puede ejecutar otra consulta en el mismo identificador de instrucciones. Si una aplicación determina que no es necesario para recuperar todas las filas de un conjunto de resultados determinado, puede cancelar el resto del conjunto de resultados por una llamada a [SQLMoreResults](../native-client-odbc-api/sqlmoreresults.md) o [SQLCloseCursor](../native-client-odbc-api/sqlclosecursor.md).  
  
 Si, en una aplicación ODBC, debe ejecutar varias veces la misma instrucción SQL con datos diferentes, utilice en la construcción de la instrucción SQL un marcador de parámetros denotado por un signo de interrogación (?)  
  
```  
INSERT INTO MyTable VALUES (?, ?, ?)  
```  
  
 Cada marcador de parámetro, a continuación, se puede enlazar a una variable de programa mediante una llamada a [SQLBindParameter](../native-client-odbc-api/sqlbindparameter.md).  
  
 Una vez ejecutadas todas las instrucciones SQL y procesados sus conjuntos de resultados, la aplicación libera el identificador de instrucción.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client es compatible con varios identificadores de instrucciones por identificador de conexión. Las transacciones se administran en el nivel de conexión, para que todo el trabajo realizado en todos los identificadores de instrucciones de una única conexión se administre como parte de la misma transacción.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Asignar un identificador de instrucción](allocating-a-statement-handle.md)  
  
-   [Crear una instrucción SQL &#40;ODBC&#41;](constructing-an-sql-statement-odbc.md)  
  
-   [Crear instrucciones SQL para cursores](constructing-sql-statements-for-cursors.md)  
  
-   [Usar parámetros de instrucciones](using-statement-parameters.md)  
  
-   [Ejecución de instrucciones &#40;ODBC&#41;](executing-statements/executing-statements-odbc.md)  
  
-   [Liberar un identificador de instrucción](freeing-a-statement-handle.md)  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Native Client &#40;ODBC&#41;](../native-client/odbc/sql-server-native-client-odbc.md)  
  
  
