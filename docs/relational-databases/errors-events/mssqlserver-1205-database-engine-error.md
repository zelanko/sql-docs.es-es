---
title: MSSQLSERVER_1205 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 1205 (Database Engine error)
ms.assetid: 9fe3f67c-df3c-4642-a3a4-ccc0e138b632
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 402d3a3cdb3d1c8eb52feaede9ff1115e745c563
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "68116032"
---
# <a name="mssqlserver_1205"></a>MSSQLSERVER_1205
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|1205|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|LK_VICTIM|  
|Texto del mensaje|La transacción (Id. de proceso %d) quedó en interbloqueo en %.*ls recursos con otro proceso y fue elegida como sujeto del interbloqueo. Vuelva a ejecutar la transacción.|  
  
## <a name="explanation"></a>Explicación  
El orden en el que se accede a los recursos en transacciones independientes es conflictivo y provoca un interbloqueo. Por ejemplo:  
  
-   Transaction1 actualiza **Table1.Row1**, mientras que Transaction2 actualiza **Table2.Row2**.  
  
-   Transaction1 intenta actualizar **Table2.Row2**, pero se bloquea porque todavía no se ha confirmado Transaction2.  
  
-   Transaction2 ahora intenta actualizar **Table1.Row1**, pero se bloquea porque no se ha confirmado Transaction1.  
  
-   Se produce un interbloqueo porque Transacción1 está esperando a que Transacción2 finalice, pero Transacción2 está esperando a que finalice Transacción1.  
  
El sistema detectará dicho interbloqueo, elegirá una de las transacciones implicadas como "víctima" y generará este mensaje, lo que deshará la transacción de la víctima.  
  
## <a name="user-action"></a>Acción del usuario  
Ejecute de nuevo la transacción. También puede revisar la aplicación para evitar los interbloqueos. La transacción elegida como víctima se puede volver a intentar y probablemente se realizará correctamente, en función de qué operaciones se estén ejecutando simultáneamente.  
  
Para evitar la aparición de interbloqueos, considere la posibilidad de hacer que todas las transacciones accedan a las filas en el mismo orden (**Table1**, seguida de **Table2**); de esta forma, aunque se puedan producir bloqueos, no se generarán interbloqueos.  
  
