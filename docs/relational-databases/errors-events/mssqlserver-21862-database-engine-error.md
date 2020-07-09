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
ms.openlocfilehash: 00a6528a223306e5a20eb29f121eb45442eb95f5
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85780542"
---
# <a name="mssqlserver_21862"></a>MSSQLSERVER_21862
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalles  
  
| Atributo | Value |  
| :-------- | :---- |  
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
  
