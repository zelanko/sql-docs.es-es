---
title: Heurística del modo AUTO para dar forma al XML devuelto | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- AUTO FOR XML mode, heuristics in shaping returned XML
ms.assetid: 6c5cb6c1-2921-4ba1-8100-0bf8074f9103
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 86e03044d610d109906ae6bfc1f0408eeb72ba8d
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2018
ms.locfileid: "43890171"
---
# <a name="auto-mode-heuristics-in-shaping-returned-xml"></a>Heurística del modo AUTO para dar forma al XML devuelto
  El modo AUTO determina la forma del XML devuelto en función de la consulta. Al determinar cómo se anidan los elementos, la heurística del modo AUTO compara los valores de columna de filas adyacentes. Se comparan columnas de todos los tipos, excepto **ntext**, **text**, **image**y **xml**. Se comparan columnas de tipo **(n)varchar(max)** y **varbinary(max)** .  
  
 El siguiente ejemplo muestra la heurística del modo AUTO que determina la forma del XML resultante:  
  
```  
SELECT T1.Id, T2.Id, T1.Name  
FROM   T1, T2  
WHERE ...  
FOR XML AUTO  
ORDER BY T1.Id  
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
  
```  
<T1 Id="1" Name="Andrew">  
    <T2 Id="2" />  
    <T2 Id="3" />  
</T1>  
<T1 Id="1" Name="Nancy" >  
      <T2 Id="4" />  
</T>  
```  
  
 Imagine ahora que la columna Name es de tipo **text** . La heurística del modo AUTO no compara los valores para este tipo. En su lugar, asume que los valores no son los mismos. Esto genera el siguiente XML:  
  
```  
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
  
## <a name="see-also"></a>Vea también  
 [Usar el modo AUTO con FOR XML](use-auto-mode-with-for-xml.md)  
  
  
