---
title: Solucionadores basados en Microsoft COM | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- COM-based resolvers [SQL Server replication]
- custom resolvers [SQL Server replication]
ms.assetid: a6637e4b-4e6b-40aa-bee6-39d98cc507c8
caps.latest.revision: 37
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 7ca1843763ae4847da6bbb5e93817cdafc98b756
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36105123"
---
# <a name="microsoft-com-based-resolvers"></a>Microsoft COM-Based Resolvers
  Todos los solucionadores basados en COM suministrados con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pueden controlar conflictos de actualización y, cuando así se indica, también conflictos de inserción y de eliminación. Todos pueden controlar el seguimiento de columnas; la mayor parte de ellos pueden controlar también el seguimiento de filas. Estos y todos los demás solucionadores basados en COM declaran los tipos de conflicto que pueden controlar, y el Agente de mezcla utiliza el solucionador predeterminado para los demás tipos de conflicto.  
  
 Los solucionadores se instalan durante el proceso de instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Ejecute el procedimiento almacenado **sp_enumcustomresolvers** para ver todos los solucionadores de conflictos registrados en un equipo. Al ejecutar el procedimiento, se muestra la descripción y el identificador único global (GUID) de cada solucionador en un conjunto de resultados independiente.  
  
 Para especificar una resolución, vea [Specify a Merge Article Resolver](../publish/specify-a-merge-article-resolver.md).  
  
 En la siguiente tabla se describen los atributos de los solucionadores específicos.  
  
|Nombre|Entrada necesaria|Descripción|Comentarios|  
|----------|--------------------|-----------------|--------------|  
|Solucionador de conflictos de suma de[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] |Nombre de la columna que se va a sumar. Debe tener un tipo de datos aritmético (como **int**, **smallint**, **numeric**, etc.).|El ganador del conflicto se determina a partir del valor de prioridad. Los valores de las columnas especificadas se establecen en la suma de los valores de las columnas de origen y de destino. Si se establece uno como NULL, se establecen al valor de la otra columna.|Admite solamente conflictos de actualización y seguimiento de columnas.|  
|Solucionador de conflictos de Cálculo de media de[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] |Nombre de la columna que se va a promediar. Debe tener un tipo de datos aritmético (como **int**, **smallint**, **numeric**, etc.).|El ganador del conflicto se determina a partir del valor de prioridad. Los valores de las columnas resultantes se establecen en el promedio de los valores de las columnas de origen y de destino. Si se establece uno como NULL, se establecen al valor de la otra columna.|Admite solamente conflictos de actualización y seguimiento de columnas.|  
|Solucionador de conflictos DATETIME (anterior gana) de[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] |Nombre de la columna que debe utilizarse para determinar el ganador del conflicto. Debe tener un tipo de datos **datetime** .|La columna que tiene el valor **datetime** anterior determina el ganador del conflicto. Si se establece uno como NULL, la fila que contenga el otro valor será el ganador.|Admite conflictos de actualización, seguimiento de filas y de columnas. Los valores de las columnas se comparan directamente, sin hacer ajustes para las diferentes zonas horarias.|  
|Solucionador de conflictos DATETIME (posterior gana) de[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] |Nombre de la columna que debe utilizarse para determinar el ganador del conflicto. Debe tener el tipo de datos **datetime** .|La columna que tiene el valor **datetime** posterior determina el ganador del conflicto. Si se establece uno como NULL, la fila que contenga el otro valor será el ganador.|Admite conflictos de actualización, seguimiento de filas y de columnas.|  
|Solucionador de conflictos de Máximo de[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] |Nombre de la columna que debe utilizarse para determinar el ganador del conflicto. Debe tener un tipo de datos aritmético (como **int**, **smallint**, **numeric**, etc.).|La columna que tiene el valor numérico más grande determina el ganador del conflicto. Si se establece uno como NULL, la fila que contenga el otro valor será el ganador.|Admite seguimiento de filas y de columnas.|  
|Solucionador de conflictos de Mínimo de[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] |Nombre de la columna que debe utilizarse para determinar el ganador del conflicto. Debe tener un tipo de datos aritmético (como **int**, **smallint**, **numeric**, etc.).|La columna que tiene el valor numérico menor determina el ganador del conflicto. Si se establece uno como NULL, la fila que contenga el otro valor será el ganador.|Admite conflictos de actualización, seguimiento de filas y de columnas.|  
|Solucionador de conflictos de Mezclar columnas de texto de[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] |Nombre de la columna de texto y del delimitador; por ejemplo, `@resolver_info = '[col1][===]'`.|El ganador del conflicto se determina a partir del valor de prioridad. Las columnas de texto en conflicto se establecen en el valor mezclado, formado por un prefijo común seguido por la parte única del publicador, después por el delimitador y, por último, por la parte única del suscriptor.|Admite solamente conflictos de actualización y seguimiento de columnas.|  
|Solucionador de conflictos de Suscriptor siempre gana de[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] |No tiene entradas.|El suscriptor, independientemente de si es el origen o el destino, es el ganador.|Admite todos los tipos de conflictos.|  
|Resolución de conflictos de Columna de prioridad de[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] |Nombre de la columna que debe utilizarse para determinar el ganador del conflicto. Debe tener un tipo de datos aritmético (como **int**, **smallint**, **numeric**, etc.).|La columna que tiene el valor numérico más grande determina el ganador del conflicto. Si se establece uno como NULL, la fila que contenga el otro valor será el ganador.|Admite conflictos de actualización, seguimiento de filas y de columnas.|  
|Solucionador de conflictos de Solo cargar de[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] |No tiene entradas.|Se aceptan los cambios cargados en el publicador; los cambios no se descargan en el suscriptor.|Admite todos los tipos de conflictos.|  
|Solucionador de conflictos de Solo descargar de[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] |No tiene entradas.|Se rechazan los cambios cargados en el publicador; los cambios se descargan en el suscriptor.|Admite todos los tipos de conflictos.|  
|Resolvedor de procedimientos almacenados de[!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQL Server|Nombre del procedimiento almacenado que debe utilizar el solucionador para solucionar el conflicto.|La resolución de conflictos depende de la lógica del procedimiento almacenado que se especifique.|Admite conflictos de actualización. Para obtener más información, consulte [Implementar un solucionador de conflictos personalizado para un artículo de mezcla](../implement-a-custom-conflict-resolver-for-a-merge-article.md)|  
  
## <a name="see-also"></a>Vea también  
 [Advanced Merge Replication Conflict Detection and Resolution](advanced-merge-replication-conflict-detection-and-resolution.md)   
 [sp_enumcustomresolvers &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql)  
  
  
