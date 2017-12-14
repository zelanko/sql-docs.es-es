---
title: Provocar eventos en el componente de script | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords: Script component [Integration Services], raising events
ms.assetid: bb389073-e1d0-4794-8d29-c8b293b6a5e3
caps.latest.revision: "16"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 62a4772efb1d5b70277882c460ea20d753a56b86
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="raising-events-in-the-script-component"></a>Provocar eventos en el componente de script
  Los eventos proporcionan una manera de notificar errores, advertencias y otra información, como el progreso o el estado de una tarea, al paquete contenedor. El paquete proporciona controladores de eventos para administrar las notificaciones de eventos. El componente de script puede provocar eventos mediante una llamada a los métodos en la propiedad <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A> de la clase **ScriptMain**. Para obtener más información sobre la manera en que los paquetes [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] controlan los eventos, vea [Controladores de eventos de Integration Services &#40;SSIS&#41;](../../../integration-services/integration-services-ssis-event-handlers.md).  
  
 Los eventos se pueden registrar en cualquier proveedor de registro habilitado en el paquete. Los proveedores de registro almacenan información sobre los eventos en un almacén de datos. El componente de script también puede usar el método <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> para registrar información en un proveedor de registro sin provocar un evento. Para obtener más información acerca de cómo usar el método <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A>, vea la siguiente sección.  
  
 Para provocar un evento, la tarea Script llama a uno de los siguientes métodos de la interfaz <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> expuestos por la propiedad <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A>:  
  
|Evento|Description|  
|-----------|-----------------|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireCustomEvent%2A>|Provoca un evento personalizado definido por el usuario en el paquete.|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireError%2A>|Informa al paquete de una condición de error.|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireInformation%2A>|Proporciona información al usuario.|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireProgress%2A>|Informa al paquete del progreso del componente.|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireWarning%2A>|Informa al paquete de que el componente está en un estado que garantiza la notificación del usuario, pero no es una condición de error.|  
  
 Aquí se proporciona un ejemplo simple de cómo provocar un evento Error:  
  
 `Dim myMetadata as IDTSComponentMetaData100`  
  
 `myMetaData = Me.ComponentMetaData`  
  
 `myMetaData.FireError(...)`  
  
## <a name="see-also"></a>Vea también  
 [Controladores de eventos de Integration Services &#40;SSIS&#41;](../../../integration-services/integration-services-ssis-event-handlers.md)   
 [Agregar un controlador de eventos a un paquete](http://msdn.microsoft.com/library/5e56885d-8658-480a-bed9-3f2f8003fd78)  
  
  
