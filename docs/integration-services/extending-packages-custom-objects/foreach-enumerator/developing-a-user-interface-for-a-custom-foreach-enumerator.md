---
title: Desarrollar una interfaz de usuario para un enumerador Para cada uno personalizado | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- custom user interface [Integration Services], custom foreach enumerators
- custom foreach enumerators [Integration Services], developing custom user interface
ms.assetid: 8aa4aa80-c9ba-42b3-ba87-ae5ea5d3cac3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d72d8fba0d9fbe68b14ebc06cbb8d171ef08ddd3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65724555"
---
# <a name="developing-a-user-interface-for-a-custom-foreach-enumerator"></a>Desarrollar una interfaz de usuario para un enumerador foreach personalizado

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Después de invalidar la implementación de las propiedades y los métodos de la clase base para proporcionar una funcionalidad personalizada, quizá desee crear una interfaz de usuario personalizada para el enumerador Foreach. Si no crea una interfaz de usuario personalizada, los usuarios solo pueden configurar el nuevo enumerador Foreach personalizado utilizando la ventana Propiedades.  
  
 En un ensamblado o proyecto personalizado de la interfaz de usuario, puede crear una clase que implementa <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumeratorUI>. Esta clase deriva de System.Windows.Forms.UserControl, que se utiliza normalmente para crear un control compuesto con el fin de hospedar otros controles de Windows Forms. El control que crea se muestra en el área **Configuración de enumerador** de la pestaña **Colección** del **Editor de bucles Para cada uno**.  
  
> [!IMPORTANT]  
>  Después de firmar y generar la interfaz de usuario personalizada e instalarla en la memoria caché de ensamblados global tal y como se describe en [Generar, implementar y depurar objetos personalizados](../../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md), recuerde proporcionar el nombre completo de esta clase en la propiedad <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute.UITypeName%2A> de <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute>.  
  
## <a name="coding-the-user-interface-control-class"></a>Codificar la clase Control de la interfaz de usuario  
  
### <a name="initializing-the-user-interface"></a>Inicializar la interfaz de usuario  
 Puede invalidar el método <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumeratorUI.Initialize%2A> para almacenar en memoria caché las referencias al objeto host y a las colecciones de administradores de conexión y variables definidas en el paquete.  
  
### <a name="setting-properties-on-the-user-interface-control"></a>Establecer las propiedades en el control de la interfaz de usuario  
 La clase UserControl, de la que se deriva la clase de interfaz de usuario, está ideada para su uso como un control compuesto para hospedar otros controles de Windows Forms. Dado que esta clase hospeda otros controles, puede diseñar una interfaz de usuario personalizada arrastrando y quitando controles, organizándolos, estableciendo sus propiedades y respondiendo en tiempo de ejecución a los eventos como en cualquier aplicación de formularios Windows Forms.  
  
### <a name="saving-settings"></a>Guardar los valores  
 Puede invalidar el método <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumeratorUI.SaveSettings%2A> para copiar los valores seleccionados por el usuario de los controles en las propiedades del enumerador cuando el usuario cierra el editor.  
  
## <a name="see-also"></a>Consulte también  
 [Crear un enumerador Para cada uno personalizado](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/creating-a-custom-foreach-enumerator.md)   
 [Codificar un enumerador ForEach personalizado](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/coding-a-custom-foreach-enumerator.md)  
  
  
