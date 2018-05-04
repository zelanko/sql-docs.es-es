---
title: Procedimientos | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-queries
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- stored procedures [ODBC]
- stored procedures [ODBC], about ODBC stored procedures
- ODBC applications, statements
- statements [ODBC], stored procedures
- ODBC applications, stored procedures
ms.assetid: c64d5f3a-376b-48ef-84f3-b6148ac8600a
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 8cf1504afb25807b60c6beea5dd7eecf599ccb56
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="procedures"></a>Procedimientos
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Un procedimiento almacenado es un objeto ejecutable precompilado que contiene una o más instrucciones [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Los procedimientos almacenados pueden tener parámetros de entrada y salida, y también puede generar un código de retorno de tipo entero. Una aplicación puede enumerar los procedimientos almacenados disponibles mediante funciones de catálogo.  
  
 Las aplicaciones ODBC destinadas a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] solo deberían usar la ejecución directa para llamar a un procedimiento almacenado. Cuando se conecta a versiones anteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client implementa [SQLPrepare Function](http://go.microsoft.com/fwlink/?LinkId=59360) mediante la creación de un procedimiento almacenado temporal, que se llama, a continuación, en **SQLExecute**. Agrega sobrecarga para que **SQLPrepare** crear un procedimiento almacenado temporal que solo se llama el procedimiento almacenado de destino frente a directamente el destino de ejecutar procedimiento almacenado. Incluso al conectarse a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], la preparación de una llamada requiere un viaje de ida y vuelta (round trip) adicional por la red y la generación de un plan de ejecución que llama simplemente al plan de ejecución de procedimiento almacenado.  
  
 Las aplicaciones ODBC deberían usar la sintaxis de ODBC CALL al ejecutar un procedimiento almacenado. El controlador se optimiza para usar un mecanismo de llamada a procedimiento remoto para llamar al procedimiento cuando se usa la sintaxis de ODBC CALL. Esto resulta más eficaz que el mecanismo usado para enviar una instrucción [!INCLUDE[tsql](../../../includes/tsql-md.md)] EXECUTE al servidor.  
  
 Para obtener más información, consulte [ejecutan procedimientos almacenados](../../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md).  
  
## <a name="see-also"></a>Vea también  
 [Ejecutar instrucciones & #40; ODBC & #41;](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  
  
