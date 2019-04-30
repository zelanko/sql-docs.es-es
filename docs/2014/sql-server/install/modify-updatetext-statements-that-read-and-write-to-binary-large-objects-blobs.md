---
title: Modificar instrucciones UPDATETEXT que leen y escriben en objetos binarios grandes (BLOB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- UPDATETEXT statement
- text [SQL Server], UPDATETEXT statements
ms.assetid: b85da6a7-42f6-4707-a25e-3ded8958b94f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7bcf5b59aa79e471ef0fc7949990b9782550ec32
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63267721"
---
# <a name="modify-updatetext-statements-that-read-and-write-to-binary-large-objects-blobs"></a>Modificar instrucciones UPDATETEXT que leen y escriben en objetos binarios grandes (BLOB)
  El Asesor de actualizaciones ha detectado instrucciones UPDATETEXT que leen y escriben en los mismos objetos binarios grandes (BLOB) mediante el mismo puntero de texto. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] no admite el uso de punteros de texto de esta forma.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Acción correctora  
 Copie los objetos BLOB en una tabla temporal o en una variable de tabla y, a continuación, vuelva a asignar el valor a la columna original.  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
