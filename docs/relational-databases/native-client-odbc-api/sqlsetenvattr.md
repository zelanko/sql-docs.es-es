---
title: SQLSetEnvAttr | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLSetEnvAttr function
ms.assetid: d4114571-feca-4330-b2e4-7bfd1050b812
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8d7a364e393c17fcb1f86480552899ec63c56141
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85751847"
---
# <a name="sqlsetenvattr"></a>SQLSetEnvAttr
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  La [Referencia del programador de ODBC](https://go.microsoft.com/fwlink/?LinkId=45250) define cómo deben interpretar los controladores ODBC las especificaciones del atributo **SQLSetEnvAttr** desde aplicaciones escritas para la API de ODBC 2.*x* u ODBC 3.*x* . El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client cumple esas reglas.  
  
 Uno de los atributos controlado por **SQLSetEnvAttr** es si se utilizará la agrupación de conexiones. Si se utiliza la agrupación de conexiones con el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, el parámetro *DriverCompletion* debe estar establecido en SQL_DRIVER_NOPROMPT al conectar con [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md) o **SQLConnect**.  
  
## <a name="see-also"></a>Consulte también  
 [SQLSetEnvAttr función)](https://go.microsoft.com/fwlink/?LinkId=59369)   
 [ODBC API Implementation Details](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
