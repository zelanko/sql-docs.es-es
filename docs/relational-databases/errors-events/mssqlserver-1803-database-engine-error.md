---
title: MSSQLSERVER_1803 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 1803 (Database Engine error)
ms.assetid: d4315390-82f1-4c4c-8d1b-1a4989537cca
caps.latest.revision: "17"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 013012ceb495ceb0b5b9e8fc207c9775713a8d5f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver1803"></a>MSSQLSERVER_1803
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|1803|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|NO_SPACE|  
|Texto del mensaje|Error de CREATE DATABASE. El archivo principal debe ser de al menos %d MB para que pueda almacenar una copia de la base de datos de modelos.|  
  
## <a name="explanation"></a>Explicación  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crea una base de datos realizando una copia de la base de datos de modelo. A continuación, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cambia el nombre de la copia y amplía la nueva base de datos al tamaño solicitado. En este caso, el usuario ha intentado crear una base de datos menor que la base de datos de modelo. Se ha producido un error en la operación porque la copia de la base de datos de modelo no cabe en el archivo de datos principal, ya que el archivo es menor que la citada base de datos.  
  
## <a name="user-action"></a>Acción del usuario  
Cree la base de datos utilizando un tamaño de archivo de base de datos mayor. A continuación, reduzca la base de datos si lo desea mediante el uso de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o la instrucción DBCC SHRINKDATABASE.  
  
