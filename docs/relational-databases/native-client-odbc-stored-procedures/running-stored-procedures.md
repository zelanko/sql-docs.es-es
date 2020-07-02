---
title: Ejecutar procedimientos almacenados | Microsoft Docs
description: Un procedimiento almacenado es un objeto ejecutable almacenado en una base de datos. SQL Server admite procedimientos almacenados y procedimientos almacenados extendidos.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC, stored procedures
- stored procedures [ODBC], running
- SQL Server Native Client ODBC driver, stored procedures
- stored procedures [ODBC], executing
ms.assetid: 866b6dd3-2acd-4dfb-aeca-a0352b2d4c6a
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e97f6717e59ffd873fc8505e538855e36dc0df1a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85773491"
---
# <a name="running-stored-procedures"></a>Ejecutar procedimientos almacenados
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  Un procedimiento almacenado es un objeto ejecutable almacenado en una base de datos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite lo siguiente:  
  
-   Procedimientos almacenados:  
  
     Una o más instrucciones SQL precompiladas en un procedimiento ejecutable único.  
  
-   Procedimientos almacenados extendidos:  
  
     Las bibliotecas de vínculos dinámicos (DLL) de C o C++ escritas en la API de Servicios abiertos de datos de SQL Server para los procedimientos almacenados extendidos. La API de Servicios abiertos de datos amplía las capacidades de los procedimientos almacenados para incluir código C o C++.  
  
 Cuando se ejecutan instrucciones, llamar a un procedimiento almacenado en el origen de datos (en lugar de ejecutar o preparar directamente una instrucción en la aplicación cliente) puede proporcionar lo siguiente:  
  
-   Rendimiento más alto  
  
     Las instrucciones SQL se analizan y compilan cuando se crean los procedimientos. Esta sobrecarga se reduce después cuando se ejecutan los procedimientos.  
  
-   Sobrecarga de red reducida  
  
     Ejecutar un procedimiento en lugar de enviar consultas complejas por la red puede reducir el tráfico de red. Si una aplicación ODBC utiliza la sintaxis ODBC {CALL} la sintaxis para ejecutar un procedimiento almacenado, el controlador ODBC realiza optimizaciones adicionales que eliminan la necesidad de convertir los datos de parámetros.  
  
-   Mayor coherencia   
  
     Si las reglas de una organización se implementan en un recurso central, como un procedimiento almacenado, se pueden codificar, probar y depurar una vez. De esta forma, los programadores individuales pueden utilizar procedimientos almacenados probados en lugar de desarrollar sus propias implementaciones.  
  
-   Mayor precisión  
  
     Dado que los procedimientos almacenados suelen estar desarrollados por programadores experimentados, tienden a ser más eficaces y a tener menos errores que el código desarrollado varias veces por programadores de diferentes niveles de competencia.  
  
-   Funcionalidad agregada  
  
     Los procedimientos almacenados extendidos pueden utilizar las características de C y C++ disponibles en las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
     Para obtener un ejemplo de cómo llamar a un procedimiento almacenado, vea [procesar códigos de retorno y parámetros de salida &#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/running-stored-procedures-process-return-codes-and-output-parameters.md).  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Llamar a un procedimiento almacenado](../../relational-databases/native-client-odbc-stored-procedures/calling-a-stored-procedure.md)  
  
-   [Procesar por lotes las llamadas a procedimientos almacenados](../../relational-databases/native-client-odbc-stored-procedures/batching-stored-procedure-calls.md)  
  
-   [Procesar resultados de procedimientos almacenados](../../relational-databases/native-client-odbc-stored-procedures/processing-stored-procedure-results.md)  
  
## <a name="see-also"></a>Consulte también  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)   
 [Temas de procedimientos de ejecución de procedimientos almacenados &#40;ODBC&#41;](https://msdn.microsoft.com/library/c2220182-a23d-4475-b353-77a77ab613d6)  
  
  
