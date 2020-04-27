---
title: Construir una instrucción SQL (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: fa955f31d26c87b39585ddead6bc5899a9e00679
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "68206782"
---
# <a name="constructing-an-sql-statement-odbc"></a>Crear una instrucción SQL (ODBC)
  Las aplicaciones ODBC realizan casi todos sus accesos a bases de datos ejecutando instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)]. El formato de estas instrucciones depende de los requisitos de aplicación. Pueden crearse instrucciones SQL de las siguientes formas:  
  
-   Codificadas de forma rígida  
  
     Instrucciones estáticas ejecutadas por una aplicación como una tarea fija.  
  
-   Creadas en tiempo de ejecución  
  
     Instrucciones SQL creadas en tiempo de ejecución que permiten al usuario personalizar la instrucción utilizando cláusulas comunes, como SELECT, WHERE y ORDER BY. Entre este tipo de instrucciones se incluyen las consultas ad hoc escritas por usuarios.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de cliente analiza las instrucciones SQL solo para la [!INCLUDE[ssDE](../../includes/ssde-md.md)]sintaxis de ODBC e ISO no admitida directamente por, que el controlador transforma [!INCLUDE[tsql](../../includes/tsql-md.md)]en. El resto de la sintaxis SQL se pasa a [!INCLUDE[ssDE](../../includes/ssde-md.md)] sin modificar, donde [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] determinará si se trata de código [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] válido. Este enfoque ofrece dos ventajas:  
  
-   Reducción de la sobrecarga  
  
     El procesamiento de la sobrecarga del controlador se minimiza ya que solo tiene que examinar un conjunto pequeño de las cláusulas ODBC e ISO.  
  
-   Flexibilidad  
  
     Los programadores pueden personalizar la portabilidad de sus aplicaciones. Para mejorar la portabilidad en distintas bases de datos, utilice principalmente la sintaxis ODBC e ISO. Para utilizar mejoras específicas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use la sintaxis [!INCLUDE[tsql](../../includes/tsql-md.md)] adecuada. El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client admite la [!INCLUDE[tsql](../../includes/tsql-md.md)] sintaxis completa, por lo que las aplicaciones basadas en ODBC pueden aprovechar todas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]las características de.  
  
 La lista de columnas de una instrucción SELECT solo debe incluir las columnas necesarias para realizar la tarea actual. Esto no solo hace que se reduzca la cantidad de datos enviados a través de la red, sino que también reduce el efecto de los cambios de la base de datos en la aplicación. Si una aplicación no hace referencia a una columna de una tabla, cualquier cambio que se realice en dicha columna no afectará a la aplicación.  
  
## <a name="see-also"></a>Consulte también  
 [Ejecutar consultas &#40;&#41;ODBC](executing-queries-odbc.md)  
  
  
