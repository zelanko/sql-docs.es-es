---
title: Compruebe que están posible escribir en todos los grupos de archivos durante el proceso de actualización | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- filegroups [SQL Server], writeable
- writeable filegroups [SQL Server]
ms.assetid: 2985efc1-4b14-46c3-abbd-a656b159f23c
caps.latest.revision: 20
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: e73899dd36a6413a2e7cdd50254049d5fcdc52ae
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103466"
---
# <a name="verify-all-filegroups-are-writeable-during-the-upgrade-process"></a>Comprobar que es posible escribir en todos los grupos de archivos durante el proceso de actualización
  El Asesor de actualizaciones ha detectado una base de datos que tiene uno o más grupos de archivos de solo lectura. Todas las bases de datos de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deben tener los grupos de archivos establecidos en READ_WRITE antes de llevar a cabo la actualización.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Acción correctora  
 Utilice ALTER DATABASE para establecer el grupo de archivos en READ_WRITE.  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
