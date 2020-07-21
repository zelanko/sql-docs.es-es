---
title: MSSQLSERVER_21862 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 21862 (Database Engine error)
ms.assetid: a1d393dd-453b-4d45-9aa5-7d371213e32b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: cc0a085886dbec7eb8e5656bd7f84b9a066a3e4f
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/21/2020
ms.locfileid: "86552173"
---
# <a name="mssqlserver_21862"></a>MSSQLSERVER_21862
    
## <a name="details"></a>Detalles  
  
|Atributo|Value|  
|-|-|  
|Nombre de producto|MSSQLSERVER|  
|Id. de evento|21862|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SQLErrorNum21862|  
|Texto del mensaje|Las columnas FILESTREAM no se pueden publicar en una publicación con el método de sincronización 'database snapshot' o 'database snapshot character'.|  
  
## <a name="explanation"></a>Explicación  
 Dado que no se puede acceder a los datos FILESTREAM mediante una instantánea de base de datos, el Agente de instantáneas no podrá leer los datos FILESTREAM cuando se especifique el parámetro *database snapshot* o *database_snapshot_character* para el método de sincronización de la publicación.  
  
## <a name="user-action"></a>Acción del usuario  
 Cambie el método de sincronización de la publicación para que no sea *database snapshot* ni *database_snapshot_character*, o simplemente excluya la columna FILESTREAM de la publicación.  
  
  
