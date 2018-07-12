---
title: Eliminar un origen de datos (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data sources [ODBC]
ms.assetid: 910e3e16-7b91-49d8-80bb-b4243926afaa
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e870254043d9cc85d99203d76513816f67267560
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37415194"
---
# <a name="delete-a-data-source-odbc"></a>Eliminar un origen de datos (ODBC)
  Puede eliminar un origen de datos con el Administrador de ODBC, mediante programación (utilizando [SQLConfigDataSource](../native-client-odbc-api/sqlconfigdatasource.md)), o mediante la eliminación de un archivo (si se trata de un nombre de origen de datos de archivo).  
  
### <a name="to-delete-a-data-source-by-using-odbc-administrator"></a>Para eliminar un origen de datos mediante el Administrador ODBC  
  
1.  En **Panel de Control**, abra **herramientas administrativas**y, a continuación, haga doble clic en **orígenes de datos (ODBC)**. Como alternativa, puede ejecutar odbcad32.exe desde el símbolo del sistema.  
  
2.  Haga clic en el **DSN de usuario**, **DSN de sistema**, o **DSN de archivo** ficha.  
  
3.  Haga clic en el origen de datos para eliminarlo.  
  
4.  Haga clic en **quitar**y, a continuación, confirme la eliminación.  
  
## <a name="example"></a>Ejemplo  
 Para eliminar mediante programación un origen de datos, llame a [SQLConfigDataSource](../native-client-odbc-api/sqlconfigdatasource.md) mediante ODBC_REMOVE_DSN u ODBC_REMOVE_SYS_DSN como segundo parámetro.  
  
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
  
## <a name="see-also"></a>Vea también  
 [Temas de procedimientos de configuración del controlador ODBC de SQL Server](../../database-engine/dev-guide/configuring-the-sql-server-odbc-driver-how-to-topics.md)  
  
  
