---
title: "Solucionadores basados en Microsoft COM | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "solucionadores basados en COM [replicación de SQL Server]"
  - "solucionadores personalizados [replicación de SQL Server]"
ms.assetid: a6637e4b-4e6b-40aa-bee6-39d98cc507c8
caps.latest.revision: 38
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Solucionadores basados en Microsoft COM
  Todos los solucionadores basados en COM suministrados con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pueden controlar conflictos de actualización y, cuando así se indica, también conflictos de inserción y de eliminación. Todos pueden controlar el seguimiento de columnas; la mayor parte de ellos pueden controlar también el seguimiento de filas. Estos y todos los demás solucionadores basados en COM declaran los tipos de conflicto que pueden controlar, y el Agente de mezcla utiliza el solucionador predeterminado para los demás tipos de conflicto.  
  
 Los solucionadores se instalan durante el proceso de instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Ejecute el **sp_enumcustomresolvers** procedimiento almacenado para ver todos los solucionadores de conflictos registrados en un equipo. Al ejecutar el procedimiento, se muestra la descripción y el identificador único global (GUID) de cada solucionador en un conjunto de resultados independiente.  
  
 Para especificar una resolución, vea [Specify a Merge Article Resolver](../../../relational-databases/replication/publish/specify-a-merge-article-resolver.md).  
  
 En la siguiente tabla se describen los atributos de los solucionadores específicos.  
  
|Nombre|Entrada necesaria|Descripción|Comentarios|  
|----------|--------------------|-----------------|--------------|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Resolución de conflictos de suma|Nombre de la columna que se va a sumar. Debe tener un tipo de datos aritmético (como **int**, **smallint**, **numérico**, y así sucesivamente).|El ganador del conflicto se determina a partir del valor de prioridad. Los valores de las columnas especificadas se establecen en la suma de los valores de las columnas de origen y de destino. Si se establece uno como NULL, se establecen al valor de la otra columna.|Admite solamente conflictos de actualización y seguimiento de columnas.|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Calcular el promedio de resolución de conflictos|Nombre de la columna que se va a promediar. Debe tener un tipo de datos aritmético (como **int**, **smallint**, **numérico**, y así sucesivamente).|El ganador del conflicto se determina a partir del valor de prioridad. Los valores de las columnas resultantes se establecen en el promedio de los valores de las columnas de origen y de destino. Si se establece uno como NULL, se establecen al valor de la otra columna.|Admite solamente conflictos de actualización y seguimiento de columnas.|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Resolución de conflictos DATETIME (anterior gana)|Nombre de la columna que debe utilizarse para determinar el ganador del conflicto. Debe tener un tipo de datos **datetime** .|La columna que tiene el valor **datetime** anterior determina el ganador del conflicto. Si se establece uno como NULL, la fila que contenga el otro valor será el ganador.|Admite conflictos de actualización, seguimiento de filas y de columnas. Los valores de las columnas se comparan directamente, sin hacer ajustes para las diferentes zonas horarias.|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Resolución de conflictos DATETIME (posterior gana)|Nombre de la columna que debe utilizarse para determinar el ganador del conflicto. Debe tener el tipo de datos **datetime** .|La columna que tiene el valor **datetime** posterior determina el ganador del conflicto. Si se establece uno como NULL, la fila que contenga el otro valor será el ganador.|Admite conflictos de actualización, seguimiento de filas y de columnas.|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Resolución de conflictos de máximo|Nombre de la columna que debe utilizarse para determinar el ganador del conflicto. Debe tener un tipo de datos aritmético (como **int**, **smallint**, **numérico**, y así sucesivamente).|La columna que tiene el valor numérico más grande determina el ganador del conflicto. Si se establece uno como NULL, la fila que contenga el otro valor será el ganador.|Admite seguimiento de filas y de columnas.|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Resolución de conflictos mínimos|Nombre de la columna que debe utilizarse para determinar el ganador del conflicto. Debe tener un tipo de datos aritmético (como **int**, **smallint**, **numérico**, y así sucesivamente).|La columna que tiene el valor numérico menor determina el ganador del conflicto. Si se establece uno como NULL, la fila que contenga el otro valor será el ganador.|Admite conflictos de actualización, seguimiento de filas y de columnas.|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Combinar a texto Solucionador de conflictos|Nombre de la columna de texto y del delimitador; por ejemplo, `@resolver_info = '[col1][===]'`.|El ganador del conflicto se determina a partir del valor de prioridad. Las columnas de texto en conflicto se establecen en el valor mezclado, formado por un prefijo común seguido por la parte única del publicador, después por el delimitador y, por último, por la parte única del suscriptor.|Admite solamente conflictos de actualización y seguimiento de columnas.|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Solucionador de conflictos de suscriptor siempre gana|No tiene entradas.|El suscriptor, independientemente de si es el origen o el destino, es el ganador.|Admite todos los tipos de conflictos.|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Resolución de conflictos de columna de prioridad|Nombre de la columna que debe utilizarse para determinar el ganador del conflicto. Debe tener un tipo de datos aritmético (como **int**, **smallint**, **numérico**, y así sucesivamente).|La columna que tiene el valor numérico más grande determina el ganador del conflicto. Si se establece uno como NULL, la fila que contenga el otro valor será el ganador.|Admite conflictos de actualización, seguimiento de filas y de columnas.|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Solucionador de conflictos de sólo cargar|No tiene entradas.|Se aceptan los cambios cargados en el publicador; los cambios no se descargan en el suscriptor.|Admite todos los tipos de conflictos.|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Solucionador de conflictos de sólo descargar|No tiene entradas.|Se rechazan los cambios cargados en el publicador; los cambios se descargan en el suscriptor.|Admite todos los tipos de conflictos.|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQL Server|Nombre del procedimiento almacenado que debe utilizar el solucionador para solucionar el conflicto.|La resolución de conflictos depende de la lógica del procedimiento almacenado que se especifique.|Admite conflictos de actualización. Para obtener más información, consulte [implementar un solucionador de conflictos personalizado para un artículo de mezcla](../../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md)|  
  
## Vea también  
 [Detección y resolución de conflictos de replicación de mezcla avanzada](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [sp_enumcustomresolvers & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md)  
  
  