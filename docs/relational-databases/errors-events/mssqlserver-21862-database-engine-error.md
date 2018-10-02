---
title: MSSQLSERVER_21862 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 21862 (Database Engine error)
ms.assetid: a1d393dd-453b-4d45-9aa5-7d371213e32b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 331e07fce8dc82ee090f3e28c8281ed29514fd46
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47624715"
---
# <a name="mssqlserver21862"></a>MSSQLSERVER_21862
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|MSSQLSERVER|  
|Identificador del evento|21862|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SQLErrorNum21862|  
|Texto del mensaje|Las columnas FILESTREAM no se pueden publicar en una publicación con el método de sincronización 'database snapshot' o 'database snapshot character'.|  
  
## <a name="explanation"></a>Explicación  
Dado que no se puede acceder a los datos FILESTREAM mediante una instantánea de base de datos, el Agente de instantáneas no podrá leer los datos FILESTREAM cuando se especifique el parámetro *database snapshot* o *database_snapshot_character* para el método de sincronización de la publicación.  
  
## <a name="user-action"></a>Acción del usuario  
Cambie el método de sincronización de la publicación para que no sea *database snapshot* ni *database_snapshot_character*, o simplemente excluya la columna FILESTREAM de la publicación.  
  
