---
description: MSSQLSERVER_945
title: MSSQLSERVER_945 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 945 (Database Engine error)
ms.assetid: ee501d13-0bd9-4627-896c-ed5b1bdb88b3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2bd18aad57eed6596ff83fc5fddbb50d33cba49a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88420899"
---
# <a name="mssqlserver_945"></a>MSSQLSERVER_945
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalles  
  
| Atributo | Value |  
| :-------- | :---- |  
|Nombre de producto|SQL Server|  
|Id. de evento|945|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DB_IS_SHUTDOWN|  
|Texto del mensaje|No se puede abrir la base de datos '%.*ls', porque no es posible tener acceso a archivos, o la memoria o el espacio en disco son insuficientes.  Compruebe el registro de errores de SQL Server para obtener más información.|  
  
## <a name="explanation"></a>Explicación  
No se pudo obtener acceso a la base de datos porque faltan archivos u otros recursos.  
  
## <a name="user-action"></a>Acción del usuario  
Compruebe el registro de errores para obtener información adicional acerca del error de memoria, espacio en disco o permiso. Confirme la ubicación de los archivos .mdf y .ndf de la base de datos afectada y confirme que la cuenta usada por [!INCLUDE[ssDE](../../includes/ssde-md.md)] tiene permiso de acceso a esos archivos. Después de corregir el problema, reinicie la base de datos usando ALTER DATABASE para establecerla en ONLINE.  
  
