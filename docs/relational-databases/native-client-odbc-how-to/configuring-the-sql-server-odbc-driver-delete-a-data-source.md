---
title: Eliminar un origen de datos (ODBC) Microsoft Docs
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- data sources [ODBC]
ms.assetid: 910e3e16-7b91-49d8-80bb-b4243926afaa
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 93ea12968c92f7849876d29d31207b8028714482
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294565"
---
# <a name="configuring-the-sql-server-odbc-driver---delete-a-data-source"></a>Configurar el controlador ODBC de SQL Server: eliminar un origen de datos
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Antes de utilizar las aplicaciones ODBC con [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o una versión posterior, debe saber cómo actualizar la versión de los procedimientos almacenados del catálogo en versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y agregar, eliminar y probar los orígenes de datos.  
  
  Puede eliminar un origen de datos mediante el Administrador ODBC, mediante programación (mediante [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md)) o eliminando un archivo (si es un nombre de origen de datos de archivo).  
  
### <a name="to-delete-a-data-source-by-using-odbc-administrator"></a>Para eliminar un origen de datos mediante el Administrador ODBC  
  
1.  En **el Panel**de control , abra Herramientas **administrativas**y, a continuación, haga doble clic en Orígenes de datos ODBC **(64 bits)** u Orígenes de **datos ODBC (32 bits).** Como alternativa, puede ejecutar odbcad32.exe desde el símbolo del sistema.  
  
2.  Haga clic en la ficha **DSN de usuario**, **DSN**del sistema o **DSN** de archivo.  
  
3.  Seleccione el origen de datos que desea eliminar.  
  
4.  Haga clic en **Quitar**y, a continuación, confirme la eliminación.  

## <a name="example"></a>Ejemplo  
 Para eliminar mediante programación un origen de datos, llame a [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md) mediante ODBC_REMOVE_DSN o ODBC_REMOVE_SYS_DSN como segundo parámetro.  
  
 El ejemplo siguiente se muestra cómo se puede eliminar un origen de datos mediante programación.  
  
```  
// remove_odbc_data_source.cpp  
// compile with: ODBCCP32.lib user32.lib  
#include <iostream>  
#include \<windows.h>  
#include \<odbcinst.h>  
  
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
 [Agregue un origen de datos &#40;&#41;ODBC](../../relational-databases/native-client-odbc-how-to/configuring-the-sql-server-odbc-driver-add-a-data-source.md)  
  
  
