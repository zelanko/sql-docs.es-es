---
title: Heurística del modo AUTO para dar forma al XML devuelto | Microsoft Docs
ms.custom: fresh2019may
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- AUTO FOR XML mode, heuristics in shaping returned XML
ms.assetid: 6c5cb6c1-2921-4ba1-8100-0bf8074f9103
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||=azuresqldb-mi-current||>=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions
ms.openlocfilehash: 408589a38ae9b01777110bbab1fb3b20c380a6c6
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "68029341"
---
# <a name="auto-mode-heuristics-in-shaping-returned-xml"></a>Heurística del modo AUTO para dar forma al XML devuelto

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

El modo AUTO determina la forma del XML devuelto en función de la consulta. Al determinar cómo se anidan los elementos, la heurística del modo AUTO compara los valores de columna de filas adyacentes. Se comparan columnas de todos los tipos, excepto **ntext**, **text**, **image**y **xml**. Se comparan columnas de tipo **(n)varchar(max)** y **varbinary(max)** .  
  
 El siguiente ejemplo muestra la heurística del modo AUTO que determina la forma del XML resultante:  
  
```sql
SELECT T1.Id, T2.Id, T1.Name  
FROM   T1, T2  
WHERE ...  
ORDER BY T1.Id
FOR XML AUTO;
```  
  
 Para determinar dónde comienza un nuevo elemento <`T1`>, se comparan todos los valores de columna de T1, excepto **ntext**, **text**, **image** y **xml**, si no se especifica la clave en la tabla T1. Después imagine que la columna **Name** es de tipo **nvarchar(40)** y que la instrucción SELECT devuelve este conjunto de filas:  
  
```  
T1.Id  T1.Name  T2.Id  
-----------------------  
1       Andrew    2  
1       Andrew    3  
1       Nancy     4  
```  
  
 La heurística del modo AUTO compara todos los valores de la tabla T1, las columnas Id y Name. Puesto que las dos primeras filas tienen los mismos valores para las columnas Id y Name, se agrega al resultado un elemento \<T1> que tiene dos elementos \<T2> secundarios.  
  
 A continuación se muestra el XML devuelto:  
  
```xml
<T1 Id="1" Name="Andrew">  
    <T2 Id="2" />  
    <T2 Id="3" />  
</T1>  
<T1 Id="1" Name="Nancy" >  
      <T2 Id="4" />  
</T>  
```  
  
 Imagine ahora que la columna Name es de tipo **text** . La heurística del modo AUTO no compara los valores para este tipo. En su lugar, asume que los valores no son los mismos. Esto genera el siguiente XML:  
  
```xml
<T1 Id="1" Name="Andrew" >  
  <T2 Id="2" />  
</T1>  
<T1 Id="1" Name="Andrew" >  
  <T2 Id="3" />  
</T1>  
<T1 Id="1" Name="Nancy" >  
  <T2 Id="4" />  
</T1>  
```  
  
## <a name="see-also"></a>Consulte también  
 [Usar el modo AUTO con FOR XML](../../relational-databases/xml/use-auto-mode-with-for-xml.md)  
  
  
