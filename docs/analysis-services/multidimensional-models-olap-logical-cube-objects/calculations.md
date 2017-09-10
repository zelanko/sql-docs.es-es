---
title: "Cálculos | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
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
- calculations [Analysis Services]
- OLAP objects [Analysis Services], calculations
- MDX [Analysis Services], calculations
- calculations [Analysis Services], about calculations
- cubes [Analysis Services], calculations
ms.assetid: 6be84916-fd05-4efc-ab98-6adbbad80154
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6fa38369b12c07a47a2501bc906535b0263db2e5
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="calculations"></a>Cálculos
  Un cálculo es una expresión de expresiones multidimensionales (MDX) o la secuencia de comandos que se utiliza para definir un miembro calculado, un conjunto con nombre o una asignación con ámbito en un cubo en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Los cálculos permiten agregar objetos definidos no por los datos del cubo, sino por expresiones que pueden hacer referencia a otras partes del cubo, a otros cubos o incluso a información que se encuentra fuera de la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Los cálculos permiten ampliar las capacidades de un cubo, al aumentar la flexibilidad y la eficacia de las aplicaciones de Business Intelligence. Para obtener más información acerca de los cálculos de scripts, consulte [Introducción a Scripting de MDX en Microsoft SQL Server 2005](http://go.microsoft.com/fwlink/?LinkId=81892). Para obtener más información acerca de los problemas de rendimiento relacionados con las consultas MDX y cálculos, vea la [Guía de rendimiento de SQL Server 2005 Analysis Services](http://go.microsoft.com/fwlink/?LinkId=81621).  
  
## <a name="calculated-members"></a>Miembros calculados  
 Un miembro calculado es un miembro cuyo valor se calcula en tiempo de ejecución mediante una expresión MDX (Expresiones multidimensionales) que se especifica al definir el miembro calculado. Los miembros calculados están disponibles para las aplicaciones de Business Intelligence del mismo modo que los demás miembros. Los miembros calculados no aumentan el tamaño del cubo porque en el mismo solamente se almacenan las definiciones; los valores se calculan en la memoria cuando son necesarios para responder a una consulta.  
  
 Los miembros calculados se pueden definir para cualquier dimensión, incluida la dimensión de medidas. Los miembros calculados creados en la dimensión de medidas se denominan medidas calculadas.  
  
 Aunque los miembros calculados normalmente se basan en los datos que ya existen en un cubo, puede crear expresiones complejas si combina datos con operadores aritméticos, números y funciones. También puede usar funciones MDX, como LookupCube, para tener acceso a los datos de otros cubos de la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] incluye bibliotecas normalizadas de funciones de Visual Studio y permite usar procedimientos almacenados para recuperar datos de otros orígenes distintos a la base de datos actual de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para obtener más información sobre los procedimientos almacenados, vea [definir procedimientos almacenados](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md).  
  
 Por ejemplo, suponga que los ejecutivos de una naviera desean determinar qué tipos de carga son más rentables basándose en el beneficio por unidad de volumen. Utilizan un cubo denominado Shipments que contiene las dimensiones Cargo, Fleet y Time y las medidas Price_to_Ship, Cost_to_Ship y Volume_in_Cubic_Meters; sin embargo, el cubo no contiene ninguna medida para la rentabilidad. En el cubo, se puede crear un miembro calculado como medida que se denomine Profit_per_Cubic_Meter mediante la combinación de las medidas existentes en la siguiente expresión:  
  
```  
([Measures].[Price_to_Ship] - [Measures].[Cost_to_Ship]) /  
[Measures].[Volume_in_Cubic_Meters]  
```  
  
 Una vez creado el miembro calculado, Profit_per_Cubic_Meter aparecerá junto con otras medidas la siguiente vez que se examine el cubo Shipments.  
  
 Para crear miembros calculados, utilice la **cálculo**pestaña Diseñador de cubos. Para obtener más información, vea [crear miembros calculados](../../analysis-services/multidimensional-models/create-calculated-members.md)  
  
## <a name="named-sets"></a>Conjuntos con nombre  
 Un conjunto con nombre es una expresión de instrucción MDX CREATE SET que devuelve un conjunto. La expresión MDX se guarda como parte de la definición de un cubo en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Un conjunto con nombre se crea para reutilizarse en consultas MDX (Expresiones Multidimensionales). Un conjunto con nombre permite a los usuarios corporativos simplificar las consultas y usar un nombre de conjunto en lugar de una expresión de conjunto para expresiones de conjunto complejas utilizadas con frecuencia. **Tema relacionado:** [crear conjuntos con nombre](../../analysis-services/multidimensional-models/create-named-sets.md)  
  
## <a name="script-commands"></a>Comandos de script  
 Un comando de script es un script MDX, incluido como parte de la definición del cubo. Los comandos de script permiten realizar prácticamente cualquier acción admitida por MDX en un cubo, como asignar un ámbito a un cálculo que solamente se aplique a parte del cubo. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], scripts MDX se pueden aplicar a todo el cubo o a secciones específicas del cubo, en puntos específicos a lo largo de la ejecución de la secuencia de comandos. El comando de script predeterminado, que es la instrucción CALCULATE, rellena las celdas del cubo con datos agregados según el ámbito predeterminado.  
  
 El ámbito predeterminado es todo el cubo, pero puede definir un ámbito más restringido, denominado subcubo, y aplicar un script MDX solamente a dicho espacio de cubo. La instrucción SCOPE define el ámbito de todas las instrucciones y expresiones MDX posteriores en el script de cálculo hasta que finaliza o se vuelve a definir el ámbito. La instrucción THIS se utiliza para aplicar una expresión MDX al ámbito actual.  Puede utilizar la instrucción BACK_COLOR para especificar el color de fondo de celda de las celdas del ámbito actual, para ayudarle durante la depuración.   
  
 Por ejemplo, puede utilizar un comando de script para asignar cuotas de venta a los empleados a lo largo del tiempo y el territorio de ventas según los valores ponderados de las ventas de un período de tiempo anterior.  
  
## <a name="see-also"></a>Vea también  
 [Cálculos en modelos multidimensionales](../../analysis-services/multidimensional-models/calculations-in-multidimensional-models.md)  
  
  
