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
ms.openlocfilehash: d0d4c51bd7f4e1eca3bf57fbcfa89aec93357fb0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85723744"
---
# <a name="mssqlserver_3151"></a>MSSQLSERVER_3151
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalles  
  
| Atributo | Value |  
| :-------- | :---- |  
|Nombre de producto|SQL Server|  
|Id. de evento|3151|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|LDDB_MASTER_LOAD_FAILED|  
|Texto del mensaje|No se pudo restaurar la base de datos maestra. Cerrando SQL Server. Compruebe los registros de errores y vuelva a generar la base de datos maestra. Para obtener más información acerca de cómo volver a crear la base de datos maestra, vea los Libros en pantalla de SQL Server.|  
  
## <a name="explanation"></a>Explicación  
Se trata de un mensaje de error general que indica diversos problemas con la base de datos **maestra**.  
  
## <a name="user-action"></a>Acción del usuario  
Consulte los registros de errores para obtener más información. Para crear una base de datos **maestra** utilizable, ejecute Setup.exe con la opción REBUILDDATABASE. Para obtener más información, vea "Procedimientos: Instalar SQL Server desde el símbolo del sistema" en los Libros en pantalla de SQL Server.  
  
