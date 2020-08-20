---
description: MSSQLSERVER_611
title: MSSQLSERVER_611 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 611 (Database Engine error)
ms.assetid: ac6a213f-5c38-44ad-bc85-a62863786614
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 33076c77372ac62f154fbe5d3c60273447be99e9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88470967"
---
# <a name="mssqlserver_611"></a>MSSQLSERVER_611
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalles  
  
| Atributo | Value |  
| :-------- | :---- |  
|Nombre de producto|SQL Server|  
|Id. de evento|611|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|VAR_SIZE_TOO_BIG|  
|Texto del mensaje|No se puede insertar ni actualizar una fila porque el tamaño total de columna variable, incluida la sobrecarga, es %d bytes más del límite.|  
  
## <a name="explanation"></a>Explicación  
El tamaño máximo de la columna de variable e es mayor que el permitido por el esquema. El Error 611 se devuelve cuando la columna de variable está por encima del límite en el caso fijo cuando el formato de almacenamiento vardecimal está habilitado, o cuando el tamaño de la columna de variable está por encima del límite permitido en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para un registro de datos comprimido.  
  
## <a name="user-action"></a>Acción del usuario  
Reduzca el tamaño del registro.  
  
