---
title: Procesando resultados de procedimientos almacenados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC, stored procedures
- SQL Server Native Client ODBC driver, stored procedures
- stored procedures [ODBC], results
ms.assetid: 788ef2a4-17de-4526-960b-46bf29aafc9f
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 18ffd4adb4387d8b7bc4209cd8e8532abdd686ac
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82709543"
---
# <a name="processing-stored-procedure-results"></a>Procesar resultados de procedimientos almacenados
  Los procedimientos almacenados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tienen cuatro mecanismos que se utilizan para devolver datos:  
  
-   Cada instrucción SELECT del procedimiento genera un conjunto de resultados.  
  
-   El procedimiento puede devolver datos mediante parámetros de salida.  
  
-   Un parámetro de salida del cursor puede devolver un cursor de servidor [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   El procedimiento puede tener un código de retorno de tipo entero.  
  
 Las aplicaciones deben ser capaces de administrar todos estos resultados de los procedimientos almacenados. La instrucción CALL o EXECUTE debería incluir los marcadores de parámetros para el código de retorno y los parámetros de salida. Utilice [SQLBindParameter](../native-client-odbc-api/sqlbindparameter.md) para enlazarlos todos como parámetros de salida y el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client transferirá los valores de salida a las variables enlazadas. Los parámetros de salida y los códigos de retorno son los últimos elementos devueltos por el cliente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ; no se devuelven a la aplicación hasta que [SQLMoreResults](../native-client-odbc-api/sqlmoreresults.md) devuelve SQL_NO_DATA.  
  
 ODBC no permite enlazar parámetros de cursor [!INCLUDE[tsql](../../includes/tsql-md.md)]. Puesto que todos los parámetros de salida se deben enlazar antes de ejecutar un procedimiento, las aplicaciones ODBC no pueden llamar a ningún procedimiento almacenado [!INCLUDE[tsql](../../includes/tsql-md.md)] que contenga un parámetro de cursor de salida.  
  
## <a name="see-also"></a>Consulte también  
 [Ejecutar procedimientos almacenados](running-stored-procedures.md)  
  
  
