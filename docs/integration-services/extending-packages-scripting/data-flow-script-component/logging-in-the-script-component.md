---
description: Registrar en el componente de script
title: Registrar en el componente de script | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Script component [Integration Services], logging
ms.assetid: 17c19787-379e-43fe-9107-e36e17ecda53
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9d761fd4bd949f066a7dc0c59a69efa4a46edfff
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88430297"
---
# <a name="logging-in-the-script-component"></a>Registrar en el componente de script

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  El registro en los paquetes de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] permite guardar información detallada sobre el progreso, los resultados y los problemas de ejecución al registrar eventos predefinidos o mensajes definidos por el usuario para su análisis posterior. El componente de script puede utilizar el método <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> de la clase **ScriptMain** para registrar datos definidos por el usuario. Si está habilitado el registro y se ha seleccionado el evento **ScriptComponentLogEntry** para su registro en la pestaña **Detalles** del cuadro de diálogo **Configurar registros de SSIS**, una sola llamada al método <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> almacena la información del evento en todos los proveedores de registro configurados para la tarea Flujo de datos.  
  
 A continuación se muestra un ejemplo sencillo de registro:  
  
 `Dim bt(0) As Byte`  
  
 `Me.Log("Test Log Event", _`  
  
 `0, _`  
  
 `bt)`  
  
> [!NOTE]  
>  Si bien puede realizar registros directamente desde el componente de script, puede que le interese implementar eventos en lugar de registrarlos. Al utilizar eventos, no solamente puede habilitar el registro de mensajes de evento, sino que también puede responder al evento con controladores de eventos predeterminados o definidos por el usuario.  
  
 Para obtener más información sobre el registro, vea [Registro de Integration Services &#40;SSIS&#41;](../../../integration-services/performance/integration-services-ssis-logging.md).  
  
## <a name="see-also"></a>Consulte también  
 [Registro de Integration Services &#40;SSIS&#41;](../../../integration-services/performance/integration-services-ssis-logging.md)  
  
  
