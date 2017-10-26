---
title: MSSQLSERVER_33081 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 33081 (Database Engine error)
ms.assetid: 839705e7-fa37-4c0d-9f3f-95a9eab98bcf
caps.latest.revision: 7
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: c5c47dd2a9d349da10e876f8da486790355be125
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver33081"></a>MSSQLSERVER_33081
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|33081|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SEC_DLL_TRUST_VERIFICATION_FAILED|  
|Texto del mensaje|No se pudo cargar el proveedor de servicios criptográficos '%.*ls' debido a una firma Authenticode o una ruta de archivo no válida.  Revise los mensajes de otros errores anteriores.|  
  
## <a name="explanation"></a>Explicación  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no pudo cargar el proveedor de servicios criptográficos enumerado en el mensaje de error. Hay varios errores de la API de Windows que podrían producir este error. El búfer en anillo contiene el nombre de la API con errores y el código de error de Windows devueltos por la API. Para obtener más información, consulte la vista de sys.dm_os_ring_buffers mediante lo siguiente.  
  
```  
SELECT * FROM sys.dm_os_ring_buffers   
WHERE ring_buffer_type = 'RING_BUFFER_SECURITY_ERROR';  
```  
  
## <a name="user-action"></a>Acción del usuario  
Para estudiar el problema, busque el código de error de Windows en MSDN (http://msdn.microsoft.com/). Resuelva el error o póngase en contacto con [!INCLUDE[msCoName](../../includes/msconame-md.md)] CSS para obtener más información. Si necesita ponerse en contacto con CSS, recopile la información siguiente para nuestro personal de soporte técnico.  
  
-   El registro de errores que muestra el error de carga del proveedor de servicios criptográficos.  
  
-   La salida de la instrucción siguiente:  
  
    ```  
    SELECT * FROM sys.dm_os_ring_buffers   
    WHERE ring_buffer_type = 'RING_BUFFER_SECURITY_ERROR';  
    ```  
  
> [!NOTE]  
> Intente recopilar la información de búfer en anillo enseguida, ya que se puede perder durante un reinicio.  
  

