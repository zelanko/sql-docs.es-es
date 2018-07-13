---
title: Uso de archivos de datos y los archivos de formato | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- bulk copy [ODBC], file formats
- ODBC, functions
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [SQL Server Native Client]
- ODBC, bulk copy operations
- bulk copy [ODBC], data files
ms.assetid: c01b7155-3f0a-473d-90b7-87a97bc56ca5
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f56cb9a5bd18ca4080d16b3fa2a4fdbff0398247
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37417994"
---
# <a name="using-data-files-and-format-files"></a>Utilizar archivos de datos y archivos de formato
  El programa de copia masiva más simple hace lo siguiente:  
  
1.  Las llamadas [bcp_init](../native-client-odbc-extensions-bulk-copy-functions/bcp-init.md) especificar realice una copia masiva (establecer BCP_OUT) de una tabla o vista para un archivo de datos.  
  
2.  Las llamadas [bcp_exec](../native-client-odbc-extensions-bulk-copy-functions/bcp-exec.md) para ejecutar la operación de copia masiva.  
  
 El archivo de datos se crea en modo nativo; por tanto, los datos de todas las columnas de la tabla o la vista se almacenan en el archivo de datos con el mismo formato que en la base de datos. A continuación, se puede realizar una copia masiva del archivo en un servidor mediante estos mismos pasos y estableciendo DB_IN en lugar de DB_OUT. Esto solamente funciona si las tablas de destino y origen tienen exactamente la misma estructura. El archivo de datos resultante también se puede especificar para el **bcp** utilidad mediante el uso de la **/n** conmutador (modo nativo).  
  
 Para realizar la copia masiva del conjunto de resultados de una instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] en lugar de directamente de una tabla o vista:  
  
1.  Llame a **bcp_init** para especificar la copia masiva pero especifique NULL para el nombre de tabla.  
  
2.  Llame a [bcp_control](../native-client-odbc-extensions-bulk-copy-functions/bcp-control.md) con *eOption* establecido en BCPHINTS y *iValue* establecido en un puntero a una cadena SQLTCHAR que contiene la instrucción de Transact-SQL.  
  
3.  Llame a **bcp_exec** para ejecutar la operación de copia masiva.  
  
 La instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] puede ser cualquier instrucción que genere un conjunto de resultados. Se crea el archivo de datos que contiene el primer conjunto de resultados de la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)]. La copia masiva omite cualquier conjunto de resultados tras la primera si la instrucción de [!INCLUDE[tsql](../../includes/tsql-md.md)] genera varios conjuntos de resultados.  
  
 Para crear un archivo de datos en qué columna de datos se almacenan en un formato diferente de la tabla, llame a [bcp_columns](../native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md) para especificar cuántas columnas se cambiarán, a continuación, llame a [bcp_colfmt](../native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md) para cada columna cuyo formato desea cambiar. Esto se hace después de llamar a **bcp_init** pero antes de llamar a **bcp_exec**. **bcp_colfmt** especifica el formato en el que los datos de la columna se almacenan en el archivo de datos. Se puede usar al realizar la copia masiva dentro o fuera. También puede usar **bcp_colfmt** para establecer los terminadores de fila y columna. Por ejemplo, si los datos no contienen ningún carácter de tabulación, puede crear un archivo delimitado por tabuladores mediante el uso de **bcp_colfmt** para establecer el carácter de tabulación como el terminador de cada columna.  
  
 Cuando masivas fuera y utilizando **bcp_colfmt**, puede crear fácilmente un archivo de formato que describe el archivo de datos que ha creado mediante una llamada a [bcp_writefmt](../native-client-odbc-extensions-bulk-copy-functions/bcp-writefmt.md) después de la última llamada a **bcp_colfmt**.  
  
 Cuando copia masiva se realiza desde un archivo de datos descrito por un archivo de formato, lea el archivo de formato mediante una llamada a [bcp_readfmt](../native-client-odbc-extensions-bulk-copy-functions/bcp-readfmt.md) después **bcp_init** pero antes **bcp_exec**.  
  
 El **bcp_control** función controla varias opciones cuando se realizan copias masivas en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde un archivo de datos. **bcp_control** establece opciones, como el número máximo de errores antes de la finalización, la fila en el archivo en el que se va a iniciar la copia masiva, la fila que se detenga en y el tamaño del lote.  
  
## <a name="see-also"></a>Vea también  
 [Realizar operaciones de copia masiva &#40;ODBC&#41;](performing-bulk-copy-operations-odbc.md)  
  
  
