---
title: Construir una instrucción SQL (ODBC) | Documentos de Microsoft
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
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a3e0c9a457293c475933f9792e03317b6fe2956d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47687003"
---
# <a name="constructing-an-sql-statement-odbc"></a>Crear una instrucción SQL (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Las aplicaciones ODBC realizan casi todos sus accesos a bases de datos ejecutando instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)]. El formato de estas instrucciones depende de los requisitos de aplicación. Pueden crearse instrucciones SQL de las siguientes formas:  
  
-   Codificadas de forma rígida  
  
     Instrucciones estáticas ejecutadas por una aplicación como una tarea fija.  
  
-   Creadas en tiempo de ejecución  
  
     Instrucciones SQL creadas en tiempo de ejecución que permiten al usuario personalizar la instrucción utilizando cláusulas comunes, como SELECT, WHERE y ORDER BY. Entre este tipo de instrucciones se incluyen las consultas ad hoc escritas por usuarios.  
  
 La [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador de cliente ODBC analiza las instrucciones de SQL para la sintaxis ODBC e ISO no admitidas directamente la [!INCLUDE[ssDE](../../includes/ssde-md.md)], que transforma el controlador [!INCLUDE[tsql](../../includes/tsql-md.md)]. El resto de la sintaxis SQL se pasa a [!INCLUDE[ssDE](../../includes/ssde-md.md)] sin modificar, donde [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] determinará si se trata de código [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] válido. Este enfoque ofrece dos ventajas:  
  
-   Reducción de la sobrecarga  
  
     El procesamiento de la sobrecarga del controlador se minimiza ya que solo tiene que examinar un conjunto pequeño de las cláusulas ODBC e ISO.  
  
-   Flexibilidad  
  
     Los programadores pueden personalizar la portabilidad de sus aplicaciones. Para mejorar la portabilidad en distintas bases de datos, utilice principalmente la sintaxis ODBC e ISO. Para utilizar mejoras específicas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use la sintaxis [!INCLUDE[tsql](../../includes/tsql-md.md)] adecuada. La [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC Native Client es compatible con la completa [!INCLUDE[tsql](../../includes/tsql-md.md)] sintaxis para aplicaciones basadas en ODBC pueden aprovechar todas las características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 La lista de columnas de una instrucción SELECT solo debe incluir las columnas necesarias para realizar la tarea actual. Esto no solo hace que se reduzca la cantidad de datos enviados a través de la red, sino que también reduce el efecto de los cambios de la base de datos en la aplicación. Si una aplicación no hace referencia a una columna de una tabla, cualquier cambio que se realice en dicha columna no afectará a la aplicación.  
  
## <a name="see-also"></a>Vea también  
 [Ejecución de consultas &#40;ODBC&#41;](../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  
