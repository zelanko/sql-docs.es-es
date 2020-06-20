---
title: MSSQLSERVER_1803 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1803 (Database Engine error)
ms.assetid: d4315390-82f1-4c4c-8d1b-1a4989537cca
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 11302f882846c49c6e9998608967e7042ac9860c
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84969445"
---
# <a name="mssqlserver_1803"></a>MSSQLSERVER_1803
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|1803|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|NO_SPACE|  
|Texto del mensaje|Error de CREATE DATABASE. El archivo principal debe ser de al menos %d MB para que pueda almacenar una copia de la base de datos de modelos.|  
  
## <a name="explanation"></a>Explicación  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crea una base de datos realizando una copia de la base de datos de modelo. A continuación, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cambia el nombre de la copia y amplía la nueva base de datos al tamaño solicitado. En este caso, el usuario ha intentado crear una base de datos menor que la base de datos de modelo. Se ha producido un error en la operación porque la copia de la base de datos de modelo no cabe en el archivo de datos principal, ya que el archivo es menor que la citada base de datos.  
  
## <a name="user-action"></a>Acción del usuario  
 Cree la base de datos utilizando un tamaño de archivo de base de datos mayor. A continuación, reduzca la base de datos si lo desea mediante el uso de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o la instrucción DBCC SHRINKDATABASE.  
  
  
