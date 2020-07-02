---
title: Eliminar un origen de datos (ODBC) | Microsoft Docs
description: Obtenga información acerca de cómo eliminar un origen de datos mediante el administrador ODBC, mediante programación o mediante un archivo, antes de utilizar las aplicaciones ODBC con SQL Server 2005 o posterior.
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
ms.openlocfilehash: 8f0a9d00338356eb02db40377da6965601c34a98
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85725079"
---
# <a name="configuring-the-sql-server-odbc-driver---delete-a-data-source"></a>Configurar el controlador ODBC de SQL Server: eliminar un origen de datos
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  Antes de utilizar las aplicaciones ODBC con [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o una versión posterior, debe saber cómo actualizar la versión de los procedimientos almacenados del catálogo en versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y agregar, eliminar y probar los orígenes de datos.  
  
  Puede eliminar un origen de datos mediante el administrador ODBC, mediante programación (mediante [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md)) o eliminando un archivo (si es un nombre de origen de datos de archivo).  
  
### <a name="to-delete-a-data-source-by-using-odbc-administrator"></a>Para eliminar un origen de datos mediante el Administrador ODBC  
  
1.  En **el panel de control**, Abra **herramientas administrativas**y, a continuación, haga doble clic en orígenes de **datos ODBC (64 bits)** o en orígenes de **datos ODBC (32 bits)**. Como alternativa, puede ejecutar odbcad32.exe desde el símbolo del sistema.  
  
2.  Haga clic en la pestaña **DSN de usuario**, **DSN de sistema**o DSN de **archivo** .  
  
3.  Seleccione el origen de datos que desea eliminar.  
  
4.  Haga clic en **quitar**y confirme la eliminación.  

## <a name="example"></a>Ejemplo  
 Para eliminar un origen de datos mediante programación, llame a [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md) utilizando ODBC_REMOVE_DSN o ODBC_REMOVE_SYS_DSN como segundo parámetro.  
  
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
 [Agregar un origen de datos &#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/configuring-the-sql-server-odbc-driver-add-a-data-source.md)  
  
  
