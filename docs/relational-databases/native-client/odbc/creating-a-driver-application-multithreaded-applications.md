---
title: Aplicaciones multiproceso con comportamiento | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client|ODBC
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- threads [SQL Server], multithreaded applications
- ODBC applications, multithreaded applications
- asynchronous operations [SQL Server Native Client]
- SQL Server Native Client ODBC driver, multithreaded applications
- multithreaded applications [SQL Server Native Client]
ms.assetid: d352c91a-6e08-4e50-9f3e-a37892d9c2cc
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d557b9195e14f4546d8b003f52bebdb7f0c2065b
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37419504"
---
# <a name="creating-a-driver-application---multithreaded-applications"></a>Crear una aplicación de controlador: aplicaciones multiproceso
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  El controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client es un controlador multiproceso. Escribir una aplicación multiproceso es una alternativa al uso de llamadas asincrónicas para procesar varias llamadas ODBC. Un subproceso puede realizar una llamada ODBC sincrónica y otros subprocesos pueden procesar mientras el primero subproceso está bloqueado en espera a la respuesta a su llamada. Este modelo es más eficaz que la realización de llamadas asincrónicas porque elimina la sobrecarga como el tráfico de red y la realización de llamadas de función ODBC que comprueban SQL_STILL_EXECUTING.  
  
 El modo asincrónico todavía es un método efectivo de procesamiento. Las mejoras de rendimiento de un modelo multiproceso no son suficientes para justificar el hecho de sobrescribir aplicaciones asincrónicas. Si los usuarios están convirtiendo aplicaciones de DB-Library que usan el modelo asincrónico de DB-Library, es más fácil convertirlas en el modelo asincrónico de ODBC.  
  
## <a name="see-also"></a>Vea también  
 [Crear una aplicación de controlador ODBC de SQL Server Native Client](../../../relational-databases/native-client/odbc/creating-a-driver-application.md)  
  
  
