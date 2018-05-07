---
title: Orígenes de datos SQL Server Native Client ODBC | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-communication
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ODBC data sources, about data sources
- ODBC data sources, names
- data sources [SQL Server Native Client]
- names [ODBC]
- ODBC applications, data sources
- SQL Server Native Client ODBC driver, data sources
- ODBC data sources
ms.assetid: a6a50fd0-d439-43fd-b76f-16ec02f478c5
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 9c79b6afa9fa88c961fff32021296cceb25d9e66
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sql-server-native-client-odbc-data-sources"></a>Orígenes de datos de ODBC para SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Un nombre del origen de datos (DSN) de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] identifica un origen de datos ODBC que contiene toda la información que una aplicación ODBC necesita para conectar a una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un servidor concreto. Existen dos métodos que puede utilizar para definir un nombre del origen de datos ODBC:  
  
-   En un equipo cliente, abra Herramientas administrativas en el Panel de Control y haga doble clic en **orígenes de datos (ODBC)**. Así abrirá el Administrador de orígenes de datos ODBC, que puede utilizar para crear un DSN.  
  
-   En una aplicación ODBC, llame a [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md).  
  
 Un origen de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contiene:  
  
-   El nombre del origen de datos.  
  
-   Cualquier información necesaria para conectar a una instancia concreta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   La base de datos predeterminada que se utilizará en una instancia concreta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (opcional).  
  
-   Valores como las opciones ANSI que se van a utilizar, si se registran estadísticas de rendimiento, etc. (opcional).  
  
 No es necesario contar con una aplicación ODBC para conectar a través de un origen de datos. Sin embargo, la aplicación debe proporcionar la misma información de conectividad a una función de conexión de ODBC que el controlador encontraría en un DSN.  
  
## <a name="see-also"></a>Vea también  
 [Comunicar con SQL Server &#40;ODBC&#41;](../../relational-databases/native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
  
