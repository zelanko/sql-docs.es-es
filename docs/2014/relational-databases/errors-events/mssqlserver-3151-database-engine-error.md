---
title: MSSQLSERVER_3151 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3151 (Database Engine error)
ms.assetid: a8657a91-ec75-4649-a09a-21920e0030ff
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 18db8cfd54a9df36564d64c0cd94407bfefb21f5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48134711"
---
# <a name="mssqlserver3151"></a>MSSQLSERVER_3151
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|3151|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|LDDB_MASTER_LOAD_FAILED|  
|Texto del mensaje|No se pudo restaurar la base de datos maestra. Cerrando SQL Server. Compruebe los registros de errores y vuelva a generar la base de datos maestra. Para obtener más información acerca de cómo volver a crear la base de datos maestra, vea los Libros en pantalla de SQL Server.|  
  
## <a name="explanation"></a>Explicación  
 Se trata de un mensaje de error general que indica diversos problemas con la base de datos **maestra**.  
  
## <a name="user-action"></a>Acción del usuario  
 Consulte los registros de errores para obtener más información. Para crear una base de datos **maestra** utilizable, ejecute Setup.exe con la opción REBUILDDATABASE. Para obtener más información, vea "Cómo instalar SQL Server desde el símbolo del sistema" en los Libros en pantalla de SQL Server.  
  
  
