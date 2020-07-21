---
title: Eliminar un origen de datos (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- data sources [ODBC]
ms.assetid: 910e3e16-7b91-49d8-80bb-b4243926afaa
author: rothja
ms.author: jroth
ms.openlocfilehash: ddb4cacd31b08346d64b3d9caa4868c53a90050d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85018963"
---
# <a name="delete-a-data-source-odbc"></a>Eliminar un origen de datos (ODBC)
  Puede eliminar un origen de datos mediante el administrador ODBC, mediante programación (mediante [SQLConfigDataSource](../native-client-odbc-api/sqlconfigdatasource.md)) o eliminando un archivo (si es un nombre de origen de datos de archivo).  
  
### <a name="to-delete-a-data-source-by-using-odbc-administrator"></a>Para eliminar un origen de datos mediante el Administrador ODBC  
  
1.  En el **Panel de control**, Abra **herramientas administrativas**y, a continuación, haga doble clic en **orígenes de datos (ODBC)**. Como alternativa, puede ejecutar odbcad32.exe desde el símbolo del sistema.  
  
2.  Haga clic en la pestaña **DSN de usuario**, **DSN de sistema**o DSN de **archivo** .  
  
3.  Haga clic en el origen de datos para eliminarlo.  
  
4.  Haga clic en **quitar**y confirme la eliminación.  
  
## <a name="example"></a>Ejemplo  
 Para eliminar un origen de datos mediante programación, llame a [SQLConfigDataSource](../native-client-odbc-api/sqlconfigdatasource.md) utilizando ODBC_REMOVE_DSN o ODBC_REMOVE_SYS_DSN como segundo parámetro.  
  
 El ejemplo siguiente se muestra cómo se puede eliminar un origen de datos mediante programación.  
  
```  
// remove_odbc_data_source.cpp  
// compile with: ODBCCP32.lib user32.lib  
#include <iostream>  
#include <windows.h>  
#include <odbcinst.h>  
  
int main() {   
   LPCSTR provider = "SQL Server";   // Windows SQL Server Driver  
   LPCSTR provider = "SQL Server";   // Windows SQL Server driver  
   LPCSTR provider2 = "SQL Server Native Client 11.0";   // SQL Server 2012 Native Client driver  
   LPCSTR dsnname = "DSN=data2";  
   BOOL retval = SQLConfigDataSource(NULL, ODBC_REMOVE_DSN, provider, dsnname);  
   std::cout << retval;   // 1 if successful  
}  
```  
  
## <a name="see-also"></a>Consulte también  
 [Temas de procedimientos de configuración del controlador ODBC de SQL Server](../../database-engine/dev-guide/configuring-the-sql-server-odbc-driver-how-to-topics.md)  
  
  
