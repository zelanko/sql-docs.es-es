---
title: MSSQLSERVER_9532 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 9532 (Database Engine error)
ms.assetid: ab95cce8-4f97-4aea-a746-a73eea7c9aab
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6cb06f095b51d4fb5e10f571d8918ffbb20c67ce
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "67903830"
---
# <a name="mssqlserver_9532"></a>MSSQLSERVER_9532
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|9532|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|XMLERR_COLUMNSET_CANNOT_CONVERT_FROM_TO|  
|Texto del mensaje|En la operación consulta/DML que implica al conjunto de columnas "%.*ls", no se pudo convertir el tipo de datos "%ls" al tipo "%ls" para la columna "%.\*ls".|  
  
## <a name="explanation"></a>Explicación  
Un conjunto de columnas es una representación XML sin tipo que combina algunas columnas de una tabla en una salida estructurada. Cuando se insertan o actualizan valores de columnas dispersas mediante el conjunto de columnas XML, los valores que se insertan en las columnas dispersas subyacentes se convierten de manera implícita del tipo de datos **xml**. Se proporcionó un valor que no se puede convertir al tipo de datos de la columna.  
  
## <a name="user-action"></a>Acción del usuario  
Dado que el valor proporcionado no se pudo convertir de manera implícita, podría ser una entrada no válida. Corrija el error e inténtelo de nuevo. Si el valor es correcto, modifique la instrucción para utilizar las columnas individuales en lugar del conjunto de columnas. Esto permitirá convertir de manera explícita el valor al tipo de datos correcto.  
  
