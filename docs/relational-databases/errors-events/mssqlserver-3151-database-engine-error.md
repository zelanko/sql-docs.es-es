---
title: MSSQLSERVER_3151 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3151 (Database Engine error)
ms.assetid: a8657a91-ec75-4649-a09a-21920e0030ff
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 068f4737a3367acdd01862cc800a4255a472c843
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "68001910"
---
# <a name="mssqlserver_3151"></a>MSSQLSERVER_3151
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|3151|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|LDDB_MASTER_LOAD_FAILED|  
|Texto del mensaje|No se pudo restaurar la base de datos maestra. Cerrando SQL Server. Compruebe los registros de errores y vuelva a generar la base de datos maestra. Para obtener más información acerca de cómo volver a crear la base de datos maestra, vea los Libros en pantalla de SQL Server.|  
  
## <a name="explanation"></a>Explicación  
Se trata de un mensaje de error general que indica diversos problemas con la base de datos **maestra**.  
  
## <a name="user-action"></a>Acción del usuario  
Consulte los registros de errores para obtener más información. Para crear una base de datos **maestra** utilizable, ejecute Setup.exe con la opción REBUILDDATABASE. Para obtener más información, vea "Cómo instalar SQL Server desde el símbolo del sistema" en los Libros en pantalla de SQL Server.  
  
