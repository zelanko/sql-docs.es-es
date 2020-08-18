---
description: MSSQLSERVER_102
title: MSSQLSERVER_102 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 102 (Database Engine error)
ms.assetid: 264dc1a2-c8a0-4c89-b5f6-951baf950299
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d18d07aae0e07625bb75c42ce60fa5c995937e10
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88339381"
---
# <a name="mssqlserver_102"></a>MSSQLSERVER_102
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalles  
  
| Atributo | Value |  
| :-------- | :---- |  
|Nombre de producto|SQL Server|  
|Id. de evento|102|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|P_SYNTAXERR2|  
|Texto del mensaje|Sintaxis incorrecta cerca de '%.*ls'.|  
  
## <a name="explanation"></a>Explicación  
Indica un error de sintaxis. La información adicional no está disponible porque el error impide que [!INCLUDE[ssDE](../../includes/ssde-md.md)] procese la instrucción.  
  
Puede deberse a un intento de crear una clave simétrica mediante el cifrado RC4 desusado o RC4_128, cuando no está en el modo de compatibilidad 90 o 100.  
  
## <a name="user-action"></a>Acción del usuario  
Busque la instrucción de [!INCLUDE[tsql](../../includes/tsql-md.md)] para los errores de sintaxis.  
  
Si creó una clave simétrica mediante RC4 o RC4_128, seleccione un cifrado más reciente como, por ejemplo, uno de los algoritmos de AES. (Se recomienda). Si debe usar RC4, emplee ALTER DATABASE SET COMPATIBILITY_LEVEL para establecer el nivel de compatibilidad de la base de datos en 90 o 100. (No se recomienda).  
  
