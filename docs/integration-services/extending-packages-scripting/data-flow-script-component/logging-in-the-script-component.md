---
title: "El componente de Script de inicio de sesión | Documentos de Microsoft"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Script component [Integration Services], logging
ms.assetid: 17c19787-379e-43fe-9107-e36e17ecda53
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 410a2472399574753d67a44b93437b1698c8b086
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="logging-in-the-script-component"></a>Registrar en el componente de script
  El registro en los paquetes de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] permite guardar información detallada sobre el progreso, los resultados y los problemas de ejecución al registrar eventos predefinidos o mensajes definidos por el usuario para su análisis posterior. Puede usar el componente de Script el <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> método de la **ScriptMain** clase para registrar datos definidos por el usuario. Si está habilitado el registro y la **ScriptComponentLogEntry** se selecciona el evento para su registro en el **detalles** pestaña de la **configurar registros de SSIS** cuadro de diálogo, una sola llamada a la <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> método almacena la información de eventos en todos los proveedores de registro que se han configurado para la tarea de flujo de datos.  
  
 A continuación se muestra un ejemplo sencillo de registro:  
  
 `Dim bt(0) As Byte`  
  
 `Me.Log("Test Log Event", _`  
  
 `0, _`  
  
 `bt)`  
  
> [!NOTE]  
>  Si bien puede realizar registros directamente desde el componente de script, puede que le interese implementar eventos en lugar de registrarlos. Al utilizar eventos, no solamente puede habilitar el registro de mensajes de evento, sino que también puede responder al evento con controladores de eventos predeterminados o definidos por el usuario.  
  
 Para obtener más información acerca del registro, consulte [Integration Services &#40; SSIS &#41; Registro](../../../integration-services/performance/integration-services-ssis-logging.md).  
  
## <a name="see-also"></a>Vea también  
 [Integration Services &#40; SSIS &#41; Registro](../../../integration-services/performance/integration-services-ssis-logging.md)  
  
  

