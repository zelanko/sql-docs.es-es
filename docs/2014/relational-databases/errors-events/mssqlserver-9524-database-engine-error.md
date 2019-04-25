---
title: MSSQLSERVER_9524 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 9524 (Database Engine error)
ms.assetid: 12da7931-e124-4466-889c-046f1b7b7bfd
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 16f5876211a987dff593721310ee31667d428b81
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62761666"
---
# <a name="mssqlserver9524"></a>MSSQLSERVER_9524
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  
