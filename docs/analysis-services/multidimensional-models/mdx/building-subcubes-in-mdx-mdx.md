---
title: "Generar subcubos en MDX (MDX) | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "consultas [MDX], subcubos"
  - "subcubos [MDX]"
  - "vistas filtradas [MDX]"
  - "MDX [Analysis Services], subcubes"
  - "expresiones multidimensionales [Analysis Services], subcubos"
  - "CREATE SUBCUBE, instrucción"
ms.assetid: 5403a62b-99ac-4d83-b02a-89bf78bf0f46
caps.latest.revision: 31
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 31
---
# Generar subcubos en MDX (MDX)
  Un subcubo es un subconjunto de un cubo en la representación de una vista filtrada de los datos subyacentes. El hecho de limitar un cubo a un subcubo permite mejorar el rendimiento de las consultas.  
  
 Para definir un subcubo se puede utilizar la instrucción [CREATE SUBCUBE](../Topic/CREATE%20SUBCUBE%20Statement%20\(MDX\).md) , tal como se describe en este tema.  
  
## Sintaxis de CREATE SUBCUBE  
 Utilice la siguiente sintaxis para crear un subcubo:  
  
```  
CREATE SUBCUBE Subcube_Identifier AS Subcube_Expression  
```  
  
 La sintaxis de CREATE SUBCUBE es relativamente sencilla. El parámetro *Subcube_Identifier* identifica el cubo en el que se basará el subcubo. El parámetro *Subcube_Expression* selecciona la parte del cubo que se convertirá en el subcubo.  
  
 Una vez creado el subcubo, éste se convierte en el contexto de todas las consultas MDX hasta que termine la sesión o hasta que se ejecute la instrucción [DROP SUBCUBE](../Topic/DROP%20SUBCUBE%20Statement%20\(MDX\).md) .  
  
### Contenido de un subcubo  
 Aunque la instrucción CREATE SUBCUBE resulte fácil de usar, la instrucción en sí no muestra explícitamente todos los miembros que pasarán a formar parte de un subcubo. La definición de los subcubos se rige por las siguientes reglas:  
  
-   Si se incluye el miembro **(Todos)** de una jerarquía, se deben incluir todos los miembros de la misma.  
  
-   Cuando se incluye un miembro se deben incluir todos sus antecesores y descendientes.  
  
-   Si se incluyen todos los miembros de un nivel, se deben incluir todos los miembros de la jerarquía. Los miembros de otras jerarquías quedan excluidos cuando no existen con miembros del nivel (por ejemplo, una jerarquía desequilibrada como puede ser una ciudad que no incluya clientes).  
  
-   Un subcubo siempre contiene todos los miembros **(Todos)** del cubo.  
  
 Otra característica es el cálculo visual del total de los valores agregados del subcubo. Por ejemplo, imaginemos un subcubo que incluya `USA`, `WA`y `OR`. El valor agregado de `USA` será la suma de `{WA,OR}` puesto que `WA` y `OR` son los únicos estados definidos por el subcubo. El resto de los estados se ignoran.  
  
 Las referencias explícitas a las celdas externas al subcubo devuelven valores de celda cuya evaluación se efectúa en el contexto del cubo completo. Por ejemplo, imagine un subcubo limitado al año en curso. Utiliza la función [ParallelPeriod](../../../mdx/parallelperiod-mdx.md) para comparar el año actual con el anterior. El resultado será la diferencia de los valores, incluso si el valor del año anterior no pertenece al subcubo.  
  
 Por último, si no se sobrescribe el contexto original, las funciones de conjuntos evaluadas en una subselección se evalúan en el contexto de dicha subselección. En caso de que se sobrescriba el contexto, las funciones de conjunto se evalúan en el contexto del cubo completo.  
  
## Ejemplo de CREATE SUBCUBE  
 En el siguiente ejemplo se crea un subcubo que restringe el cubo Budget a las cuentas 4200 y 4300:  
  
 `CREATE SUBCUBE Budget AS SELECT {[Account].[Account].&[4200], [Account].[Account].&[4300] } ON 0 FROM Budget`  
  
 Al haber creado un subcubo para la sesión, las consultas que se realicen a partir de ahora se efectuarán en el subcubo, no en el cubo completo. Por ejemplo, ejecute la siguiente consulta. La consulta solo devolverá los miembros de las cuentas 4200 y 4300.  
  
 `SELECT [Account].[Account].Members ON 0, Measures.Members ON 1 FROM Budget`  
  
## Vea también  
 [Establecer el contexto de cubo en una consulta &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/establishing-cube-context-in-a-query-mdx.md)   
 [Aspectos básicos de las consultas MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  