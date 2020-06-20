---
title: MSSQLSERVER_3961 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3961 (Database Engine error)
ms.assetid: 3bbc6965-6445-400c-940a-2d85b037513f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f55be9288b3c2e559633d0f67709829466fc8815
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85033364"
---
# <a name="mssqlserver_3961"></a>MSSQLSERVER_3961
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|3961|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|XACT_METADATA_INVALID|  
|Texto del mensaje|Error de la transacción de aislamiento de instantánea en la base de datos '%. * ls' porque el objeto al que tuvo acceso la instrucción ha sido modificado por una instrucción DDL de otra transacción simultánea desde el inicio de esta transacción.  Está deshabilitada porque los metadatos no tienen versiones. Una actualización simultánea de los metadatos puede dar lugar a incoherencias si se combina con el aislamiento de la instantánea.|  
  
## <a name="explanation"></a>Explicación  
 Este error se puede producir durante una consulta de metadatos en una transacción de aislamiento de la instantánea si una instrucción DDL simultánea actualiza los metadatos a los que esta transacción está accediendo. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no permite controlar las versiones de los metadatos. Por este motivo, hay restricciones en las operaciones de DDL que se pueden realizar en una transacción explícita que se ejecuta con aislamiento de la instantánea. Una transacción implícita, por definición, es una única instrucción que hace que sea posible aplicar la semántica del aislamiento de la instantánea incluso con instrucciones DDL. Las instrucciones de DDL siguientes no se admiten bajo el aislamiento de instantánea después de una instrucción BEGIN TRANSACTION: ALTER TABLE, CREATE INDEX, CREATE XML INDEX, ALTER INDEX, DROP INDEX, DBCC REINDEX, ALTER PARTITION FUNCTION, ALTER PARTITION SCHEME, ni ninguna instrucción de DDL de Common Language Runtime (CLR). Estas instrucciones se permiten cuando usa el aislamiento de la instantánea en transacciones implícitas. Una transacción implícita, por definición, es una única instrucción que hace que sea posible aplicar la semántica del aislamiento de la instantánea incluso con instrucciones DDL.  
  
## <a name="user-action"></a>Acción del usuario  
 Antes de consultar los metadatos, cambie el nivel de aislamiento a un nivel que no sea de aislamiento como, por ejemplo, lectura confirmada.  
  
  
