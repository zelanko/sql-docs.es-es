---
title: Construir una instrucción SQL (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, statements
- statements [ODBC], constructing
- ODBC applications, statements
ms.assetid: 0acc71e2-8004-4dd8-8592-05c022bdd692
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 96e3c04692360bd13010fe40063b0e761d60b2ce
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2019
ms.locfileid: "73779980"
---
# <a name="constructing-an-sql-statement-odbc"></a>Crear una instrucción SQL (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Las aplicaciones ODBC realizan casi todos sus accesos a bases de datos ejecutando instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)]. El formato de estas instrucciones depende de los requisitos de aplicación. Pueden crearse instrucciones SQL de las siguientes formas:  
  
-   Codificadas de forma rígida  
  
     Instrucciones estáticas ejecutadas por una aplicación como una tarea fija.  
  
-   Creadas en tiempo de ejecución  
  
     Instrucciones SQL creadas en tiempo de ejecución que permiten al usuario personalizar la instrucción utilizando cláusulas comunes, como SELECT, WHERE y ORDER BY. Entre este tipo de instrucciones se incluyen las consultas ad hoc escritas por usuarios.  
  
 El controlador ODBC de cliente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] analiza las instrucciones SQL solo para la sintaxis de ODBC y ISO no admitida directamente por el [!INCLUDE[ssDE](../../includes/ssde-md.md)], que el controlador transforma en [!INCLUDE[tsql](../../includes/tsql-md.md)]. El resto de la sintaxis SQL se pasa a [!INCLUDE[ssDE](../../includes/ssde-md.md)] sin modificar, donde [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] determinará si se trata de código [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] válido. Este enfoque ofrece dos ventajas:  
  
-   Reducción de la sobrecarga  
  
     El procesamiento de la sobrecarga del controlador se minimiza ya que solo tiene que examinar un conjunto pequeño de las cláusulas ODBC e ISO.  
  
-   Flexibilidad  
  
     Los programadores pueden personalizar la portabilidad de sus aplicaciones. Para mejorar la portabilidad en distintas bases de datos, utilice principalmente la sintaxis ODBC e ISO. Para utilizar mejoras específicas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use la sintaxis [!INCLUDE[tsql](../../includes/tsql-md.md)] adecuada. El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client admite la sintaxis de [!INCLUDE[tsql](../../includes/tsql-md.md)] completa, por lo que las aplicaciones basadas en ODBC pueden aprovechar todas las características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 La lista de columnas de una instrucción SELECT solo debe incluir las columnas necesarias para realizar la tarea actual. Esto no solo hace que se reduzca la cantidad de datos enviados a través de la red, sino que también reduce el efecto de los cambios de la base de datos en la aplicación. Si una aplicación no hace referencia a una columna de una tabla, cualquier cambio que se realice en dicha columna no afectará a la aplicación.  
  
## <a name="see-also"></a>Vea también  
 [Ejecutar consultas &#40;ODBC&#41;](../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  
