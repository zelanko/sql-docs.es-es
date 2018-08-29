---
title: SQLSetEnvAttr | Documentos de Microsoft
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLSetEnvAttr function
ms.assetid: d4114571-feca-4330-b2e4-7bfd1050b812
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b086b62e7241e3bb82b3d85fe7e83720c575d6a5
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43084326"
---
# <a name="sqlsetenvattr"></a>SQLSetEnvAttr
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  La [Referencia del programador de ODBC](http://go.microsoft.com/fwlink/?LinkId=45250) define cómo deben interpretar los controladores ODBC las especificaciones del atributo **SQLSetEnvAttr** desde aplicaciones escritas para la API de ODBC 2.*x* u ODBC 3.*x* . El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client cumple esas reglas.  
  
 Uno de los atributos controlado por **SQLSetEnvAttr** es si se utilizará la agrupación de conexiones. Si se utiliza la agrupación de conexiones con el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, el parámetro *DriverCompletion* debe estar establecido en SQL_DRIVER_NOPROMPT al conectar con [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md) o **SQLConnect**.  
  
## <a name="see-also"></a>Vea también  
 [Función SQLSetEnvAttr](http://go.microsoft.com/fwlink/?LinkId=59369)   
 [Detalles de implementación de la API de ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
