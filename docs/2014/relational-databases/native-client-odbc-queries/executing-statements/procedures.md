---
title: Procedimientos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 82f9d922d2192925033aceb6c253088ccb9f1d6f
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82700405"
---
# <a name="procedures"></a>Procedimientos
  Un procedimiento almacenado es un objeto ejecutable precompilado que contiene una o más instrucciones [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Los procedimientos almacenados pueden tener parámetros de entrada y salida, y también puede generar un código de retorno de tipo entero. Una aplicación puede enumerar los procedimientos almacenados disponibles mediante funciones de catálogo.  
  
 Las aplicaciones ODBC destinadas a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] solo deberían usar la ejecución directa para llamar a un procedimiento almacenado. Cuando se conecta a versiones anteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client implementa la [función SQLPrepare](https://go.microsoft.com/fwlink/?LinkId=59360) creando un procedimiento almacenado temporal, al que se llama a continuación en **SQLExecute**. Agrega sobrecarga para que **SQLPrepare** cree un procedimiento almacenado temporal que solo llama al procedimiento almacenado de destino, en lugar de ejecutar directamente el procedimiento almacenado de destino. Incluso al conectarse a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], la preparación de una llamada requiere un viaje de ida y vuelta (round trip) adicional por la red y la generación de un plan de ejecución que llama simplemente al plan de ejecución de procedimiento almacenado.  
  
 Las aplicaciones ODBC deberían usar la sintaxis de ODBC CALL al ejecutar un procedimiento almacenado. El controlador se optimiza para usar un mecanismo de llamada a procedimiento remoto para llamar al procedimiento cuando se usa la sintaxis de ODBC CALL. Esto resulta más eficaz que el mecanismo usado para enviar una instrucción [!INCLUDE[tsql](../../../includes/tsql-md.md)] EXECUTE al servidor.  
  
 Para obtener más información, vea [Ejecutar procedimientos almacenados](../../native-client-odbc-stored-procedures/running-stored-procedures.md).  
  
## <a name="see-also"></a>Consulte también  
 [Ejecutar instrucciones &#40;ODBC&#41;](executing-statements-odbc.md)  
  
  
