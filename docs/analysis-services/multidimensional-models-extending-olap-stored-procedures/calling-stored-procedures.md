---
title: Llamar a procedimientos almacenados | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- calling stored procedures
- stored procedures [Analysis Services], calling
- MDX queries [Analysis Services]
- CALL statement
ms.assetid: 96a9660d-875b-4ee4-b339-90020b1d9895
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9e2c8656c28db458104a3793175a739d311ac379
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="calling-stored-procedures"></a>Llamar a procedimientos almacenados
  Se puede llamar a los procedimientos almacenados desde el servidor o desde la aplicación cliente. En cualquier caso, los procedimientos almacenados siempre se ejecutan en el servidor, ya sea en el contexto del servidor o de una base de datos. No se requieren permisos específicos para ejecutar un procedimiento almacenado. Cuando un ensamblado agrega un procedimiento almacenado al contexto del servidor o de la base de datos, cualquier usuario puede ejecutarlo, siempre que el rol del usuario permita las acciones que efectúa el procedimiento almacenado.  
  
 La llamada a un procedimiento almacenado en MDX se realiza del mismo modo que la llamada a una función MDX intrínseca. Para un procedimiento almacenado que no toma parámetros, se utilizan el nombre del procedimiento y unos paréntesis vacíos, como se muestra a continuación:  
  
```  
MyStoredProcedure()  
```  
  
 Si el procedimiento almacenado toma uno o más parámetros, éstos se proporcionan por orden, separados por comas. En el siguiente ejemplo se muestra un ejemplo de procedimiento almacenado con tres parámetros:  
  
```  
MyStoredProcedure("Parameter1", 2, 800)  
```  
  
## <a name="calling-stored-procedures-in-mdx-queries"></a>Llamar a procedimientos almacenados en consultas MDX  
 En todas las consultas MDX, el procedimiento almacenado debe devolver el tipo sintácticamente correcto que requiere una expresión MDX. Si un procedimiento almacenado no devuelve el tipo correcto, se produce un error de MDX. En los siguientes ejemplos se muestran procedimientos almacenados que devuelven un conjunto, un miembro y el resultado de una operación matemática.  
  
### <a name="returning-a-set"></a>Devolver un conjunto  
 En los siguientes ejemplos se implementa un procedimiento almacenado llamado MySproc, que devuelve un conjunto. En el primer ejemplo, MySproc devuelve el conjunto directamente en la expresión SELECT. En los dos ejemplos siguientes, MySproc devuelve el conjunto como argumento de las funciones Crossjoin y DrilldownLevel.  
  
```  
SELECT MySetProcedure(a,b,c) ON 0 FROM Sales  
SELECT Crossjoin(MySetProcedure(a,b,c)) ON 0 FROM Sales  
SELECT DrilldownLevel(MySetProcedure(a,b,c)) ON 0 FROM Sales  
```  
  
### <a name="returning-a-member"></a>Devolver un miembro  
 En el siguiente ejemplo se muestra una función MySproc que devuelve un miembro:  
  
```  
SELECT Descendants(MySproc(a,b,c),3) ON 0 FROM Sales  
```  
  
### <a name="returning-the-result-of-a-math-operation"></a>Devolver el resultado de una operación matemática  
  
```  
SELECT Country.Members on 0, MySproc(Measures.Sales) ON 1 FROM Sales  
```  
  
## <a name="calling-stored-procedures-with-the-call-statement"></a>Llamar a procedimientos almacenados con la instrucción Call  
 Se pueden llamar a procedimientos almacenados fuera del contexto de una consulta MDX mediante MDX **llamar** instrucción.  
  
 Utilice este método para crear instancias de los efectos secundarios de una consulta almacenada o para que la aplicación obtenga los resultados de una consulta almacenada. Un uso común de la **llamar** instrucción sería utilizar Analysis Management Objects (AMO) para realizar funciones administrativas que no tienen un resultado devuelto. Por ejemplo, el comando siguiente llama a un procedimiento almacenado:  
  
```  
Call MyStoredProcedure(a,b,c)  
```  
  
 El único tipo admitido que devuelve desde un procedimiento almacenado en una **llamar** instrucción es un conjunto de filas. La serialización para un conjunto de filas se define mediante XML for Analysis. Si un procedimiento almacenado en una **llamar** instrucción devuelve cualquier otro tipo, se omite y no se devuelve en XML a la aplicación que realiza la llamada. Para obtener más información acerca de los conjuntos de filas de XML for Analysis, vea el tema sobre conjuntos de filas del esquema de XML for Analysis.  
  
 Si un procedimiento almacenado devuelve un conjunto de filas de .NET, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] convierte el resultado en el servidor en un conjunto de filas de XML for Analysis. Siempre se devuelve el código XML para el conjunto de filas de análisis por un procedimiento almacenado en el **llamar a** (función). Si un conjunto de datos contiene características que no se pueden expresar en el conjunto de filas de XML for Analysis, se genera un error.  
  
 También se pueden utilizar procedimientos que devuelven valores nulos (por ejemplo, subrutinas de Visual Basic) con la palabra clave CALL. Por ejemplo, si desea utilizar la función MyVoidFunction() en una instrucción MDX, se utilizaría la siguiente sintaxis:  
  
```  
CALL(MyVoidFunction)  
```  
  
## <a name="see-also"></a>Vea también  
 [Administración de ensamblados de modelos multidimensionales](../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)   
 [Definir procedimientos almacenados](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  

