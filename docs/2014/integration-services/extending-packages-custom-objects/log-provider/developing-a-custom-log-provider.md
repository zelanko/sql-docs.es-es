---
title: Desarrollar un proveedor de registro personalizado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- SSIS packages, log providers
- custom log providers [Integration Services]
- SQL Server Integration Services packages, log providers
- log providers [Integration Services]
- packages [Integration Services], logs
- Integration Services packages, log providers
ms.assetid: 3f715b95-7074-4f5c-8ae2-246998052e78
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: af3478e254f01f7cf53d5a09b6febab3b1e85e8b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "78176311"
---
# <a name="developing-a-custom-log-provider"></a>Desarrollar un proveedor de registro personalizado
  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] incluye completas capacidades de registro que permiten capturar eventos que se producen durante la ejecución del paquete. [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] incluye varios proveedores de registro que permiten crear registros y almacenarlos en formatos como XML, texto, base de datos o en el registro de eventos de Windows. Si los proveedores de registro y los formatos de salida que se proporcionan no cumplen completamente sus requisitos, puede crear un proveedor de registro personalizado.

 Para crear un proveedor de registro personalizado, debe crear una clase que herede de la clase base <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase>, aplicar el atributo <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute> a la nueva clase e invalidar los métodos y propiedades importantes de la clase base, incluidos la propiedad <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.ConfigString%2A> y el método <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Log%2A>.

## <a name="in-this-section"></a>En esta sección
 En esta sección se describe cómo crear, configurar y codificar un proveedor de registro personalizado.

 [Crear un proveedor de registro personalizado](creating-a-custom-log-provider.md) Describe cómo crear las clases para un proyecto de proveedor de registro personalizado.

 [Codificar un proveedor de registro personalizado](coding-a-custom-log-provider.md) Describe cómo implementar un proveedor de registro personalizado invalidando los métodos y las propiedades de la clase base.

 [Desarrollar una interfaz de usuario para un proveedor de registro personalizado](developing-a-user-interface-for-a-custom-log-provider.md) Las interfaces de usuario personalizadas para los proveedores de registro personalizados [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]no se admiten en.

## <a name="related-topics"></a>Temas relacionados

### <a name="information-common-to-all-custom-objects"></a>Información común a todos los objetos personalizados
 Para obtener información común a todos los tipos de objetos personalizados que puede crear en [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], vea los temas siguientes:

 [Desarrollar objetos personalizados para Integration Services](../developing-custom-objects-for-integration-services.md) Describe los pasos básicos para implementar todos los tipos de objetos personalizados [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]para.

 [Conservar objetos personalizados](../persisting-custom-objects.md) Describe la persistencia personalizada y explica cuándo es necesario.

 [Compilar, implementar y depurar objetos personalizados](../building-deploying-and-debugging-custom-objects.md) Describe las técnicas para compilar, firmar, implementar y depurar objetos personalizados.

### <a name="information-about-other-custom-objects"></a>Información sobre otros objetos personalizados
 Para obtener información sobre los demás tipos de objetos personalizados que puede crear en [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], vea los temas siguientes:

 [Desarrollar una tarea personalizada](../task/developing-a-custom-task.md) Describe cómo programar tareas personalizadas.

 [Desarrollar un administrador de conexiones personalizado](../connection-manager/developing-a-custom-connection-manager.md) Describe cómo programar administradores de conexiones personalizados.

 [Desarrollar un enumerador Foreach personalizado](../foreach-enumerator/developing-a-custom-foreach-enumerator.md) Describe cómo programar los enumeradores personalizados.

 [Desarrollar un componente de flujo de datos personalizado](../data-flow/developing-a-custom-data-flow-component.md) Describe cómo programar orígenes, transformaciones y destinos de flujo de datos personalizados.

![Integration Services icono (pequeño)](../../media/dts-16.gif "Icono de Integration Services (pequeño)")  **Manténgase al día con Integration Services**<br /> Para obtener las descargas, artículos, ejemplos y vídeos más recientes de Microsoft, así como soluciones seleccionadas de la comunidad, visite la página de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] en MSDN:<br /><br /> [Visite la página de Integration Services en MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para recibir notificaciones automáticas de estas actualizaciones, suscríbase a las fuentes RSS disponibles en la página.


