---
title: MSSQLSERVER_9524 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 9524 (Database Engine error)
ms.assetid: 12da7931-e124-4466-889c-046f1b7b7bfd
caps.latest.revision: 9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 788b5264633f1ea7dab5168f5baf71a0ea10197b
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37430164"
---
# <a name="mssqlserver9524"></a>MSSQLSERVER_9524
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|9254|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|XMLERR_INVALID_COLUMNSET_XML|  
|Texto del mensaje|El contenido XML proporcionado no tiene el formato XML requerido para conjuntos de columnas dispersas.|  
  
## <a name="explanation"></a>Explicación  
 Se ha intentado modificar un conjunto de columnas. El contenido XML de un conjunto de columnas debe satisfacer las restricciones de formato correspondientes. El formato general de un conjunto de columnas es el siguiente:  
  
 `<column_name_1>value1</column_name_1><column_name_2>value2</column_name_2>...`  
  
 Para obtener más información sobre conjuntos de columnas, vea el tema "Usar conjuntos de columnas" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="user-action"></a>Acción del usuario  
 Corrija el formato del contenido XML del conjunto de columnas en la instrucción.  
  
  
