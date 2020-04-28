---
title: Aplicaciones multiproceso | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- threads [SQL Server], multithreaded applications
- ODBC applications, multithreaded applications
- asynchronous operations [SQL Server Native Client]
- SQL Server Native Client ODBC driver, multithreaded applications
- multithreaded applications [SQL Server Native Client]
ms.assetid: d352c91a-6e08-4e50-9f3e-a37892d9c2cc
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2402c093c2abd43f4896fd2760dc9ad02b55e0f1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303778"
---
# <a name="creating-a-driver-application---multithreaded-applications"></a>Crear una aplicación del controlador: aplicaciones multiproceso
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  El controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client es un controlador multiproceso. Escribir una aplicación multiproceso es una alternativa al uso de llamadas asincrónicas para procesar varias llamadas ODBC. Un subproceso puede realizar una llamada ODBC sincrónica y otros subprocesos pueden procesar mientras el primero subproceso está bloqueado en espera a la respuesta a su llamada. Este modelo es más eficaz que la realización de llamadas asincrónicas porque elimina la sobrecarga como el tráfico de red y la realización de llamadas de función ODBC que comprueban SQL_STILL_EXECUTING.  
  
 El modo asincrónico todavía es un método efectivo de procesamiento. Las mejoras de rendimiento de un modelo multiproceso no son suficientes para justificar el hecho de sobrescribir aplicaciones asincrónicas. Si los usuarios están convirtiendo aplicaciones de DB-Library que usan el modelo asincrónico de DB-Library, es más fácil convertirlas en el modelo asincrónico de ODBC.  
  
## <a name="see-also"></a>Consulte también  
 [Crear una aplicación de controlador ODBC de SQL Server Native Client](../../../relational-databases/native-client/odbc/creating-a-driver-application.md)  
  
  
