---
title: Ejecutar procedimientos almacenados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC, stored procedures
- stored procedures [ODBC], running
- SQL Server Native Client ODBC driver, stored procedures
- stored procedures [ODBC], executing
ms.assetid: 866b6dd3-2acd-4dfb-aeca-a0352b2d4c6a
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: fb03809fb465c4b23131d2133931028d7bec118d
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82709467"
---
# <a name="running-stored-procedures"></a>Ejecutar procedimientos almacenados
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
  
     Para obtener un ejemplo de cómo llamar a un procedimiento almacenado, vea [procesar códigos de retorno y parámetros de salida &#40;ODBC&#41;](../native-client-odbc-how-to/running-stored-procedures-process-return-codes-and-output-parameters.md).  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Llamar a un procedimiento almacenado](calling-a-stored-procedure.md)  
  
-   [Procesar por lotes las llamadas a procedimientos almacenados](batching-stored-procedure-calls.md)  
  
-   [Procesar resultados de procedimientos almacenados](processing-stored-procedure-results.md)  
  
## <a name="see-also"></a>Consulte también  
 [SQL Server Native Client &#40;ODBC&#41;](../native-client/odbc/sql-server-native-client-odbc.md)   
 [Temas de procedimientos de ejecución de procedimientos almacenados &#40;ODBC&#41;](../../database-engine/dev-guide/running-stored-procedures-how-to-topics-odbc.md)  
  
  
