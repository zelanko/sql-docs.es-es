---
title: MSSQLSERVER_3271 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3271 (Database Engine error)
ms.assetid: 21b8de4b-6624-4163-9561-1a6cc8fe3d51
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b255dfb092cd15865cba0a2389a50604a29404c6
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/21/2020
ms.locfileid: "86551700"
---
# <a name="mssqlserver_3271"></a>MSSQLSERVER_3271
    
## <a name="details"></a>Detalles  
  
|Atributo|Value|  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|3271|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DMPIO_IO_ERROR|  
|Texto del mensaje|Error de E/S irrecuperable en el archivo "%ls:" %ls.|  
  
## <a name="explanation"></a>Explicación  
 Se trata de un error general que ocurre cuando el sistema operativo genera un error mientras se realiza una E/S durante una operación de copia de seguridad o de restauración. En la mayoría de los casos, la causa es simplemente que el medio de copia de seguridad está lleno.  
  
 El error puede incluir texto adicional del sistema operativo indicando que el disco está lleno. Al realizar una operación de copia de seguridad o restauración con software de copia de seguridad de otros fabricantes, puede aparecer un mensaje adicional que indica que se ha producido un error en la copia de seguridad. El mensaje puede ser similar al siguiente texto:  
  
```  
"2005-08-02 16:05:16.04 spid55 Error: 18210, Severity: 16, State: 1.  
 2005-08-02 16:05:16.04 spid55 BackupVirtualDeviceFile  
::RequestDurableMedia: Flush failure on backup device 'VDINULL'.   
Operating system error 995(The I/O operation has been aborted because   
of either a thread exit or an application request.)."  
```  
  
 Se trata de una indicación de que el software de copia de seguridad ha solicitado la finalización de la operación de copia de seguridad o de restauración.  
  
## <a name="user-action"></a>Acción del usuario  
 Realice las siguientes tareas, según corresponda:  
  
-   Revise los mensajes de error subyacentes del sistema y los mensajes de error de SQL Server anteriores a éste para identificar la causa del error.  
  
-   Asegúrese de que el medio para las copias de seguridad y restauración tenga suficiente espacio.  
  
-   Corrija cualquier error generado por el software de copias de seguridad y restauración de otros fabricantes.  
  
  
