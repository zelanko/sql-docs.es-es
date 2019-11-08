---
title: Procedimientos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- stored procedures [ODBC]
- stored procedures [ODBC], about ODBC stored procedures
- ODBC applications, statements
- statements [ODBC], stored procedures
- ODBC applications, stored procedures
ms.assetid: c64d5f3a-376b-48ef-84f3-b6148ac8600a
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 66db10c8ac64fee4e6e9ccbc405ab5b804adb32a
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2019
ms.locfileid: "73779527"
---
# <a name="procedures"></a>Procedimientos
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Un procedimiento almacenado es un objeto ejecutable precompilado que contiene una o más instrucciones [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Los procedimientos almacenados pueden tener parámetros de entrada y salida, y también puede generar un código de retorno de tipo entero. Una aplicación puede enumerar los procedimientos almacenados disponibles mediante funciones de catálogo.  
  
 Las aplicaciones ODBC destinadas a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] solo deberían usar la ejecución directa para llamar a un procedimiento almacenado. Cuando se conecta a versiones anteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], el controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client implementa la [función SQLPrepare](https://go.microsoft.com/fwlink/?LinkId=59360) creando un procedimiento almacenado temporal, al que se llama después en **SQLExecute**. Agrega sobrecarga para que **SQLPrepare** cree un procedimiento almacenado temporal que solo llama al procedimiento almacenado de destino, en lugar de ejecutar directamente el procedimiento almacenado de destino. Incluso al conectarse a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], la preparación de una llamada requiere un viaje de ida y vuelta (round trip) adicional por la red y la generación de un plan de ejecución que llama simplemente al plan de ejecución de procedimiento almacenado.  
  
 Las aplicaciones ODBC deberían usar la sintaxis de ODBC CALL al ejecutar un procedimiento almacenado. El controlador se optimiza para usar un mecanismo de llamada a procedimiento remoto para llamar al procedimiento cuando se usa la sintaxis de ODBC CALL. Esto resulta más eficaz que el mecanismo usado para enviar una instrucción [!INCLUDE[tsql](../../../includes/tsql-md.md)] EXECUTE al servidor.  
  
 Para obtener más información, vea [Ejecutar procedimientos almacenados](../../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md).  
  
## <a name="see-also"></a>Vea también  
 [Ejecutar instrucciones &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  
  
