---
title: Desarrollar una interfaz de usuario para un enumerador ForEach personalizado | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
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
- custom user interface [Integration Services], custom foreach enumerators
- custom foreach enumerators [Integration Services], developing custom user interface
ms.assetid: 8aa4aa80-c9ba-42b3-ba87-ae5ea5d3cac3
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e743464fcf482ea51f0cde78d692b367c2be525b
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="developing-a-user-interface-for-a-custom-foreach-enumerator"></a>Desarrollar una interfaz de usuario para un enumerador foreach personalizado
  Después de invalidar la implementación de las propiedades y los métodos de la clase base para proporcionar una funcionalidad personalizada, quizá desee crear una interfaz de usuario personalizada para el enumerador Foreach. Si no crea una interfaz de usuario personalizada, los usuarios solo pueden configurar el nuevo enumerador Foreach personalizado utilizando la ventana Propiedades.  
  
 En un ensamblado o proyecto personalizado de la interfaz de usuario, puede crear una clase que implementa <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumeratorUI>. Esta clase se deriva de System.Windows.Forms.UserControl, que se utiliza normalmente para crear un control compuesto para hospedar otros controles de formularios Windows Forms. El control que se crea se muestra en el **configuración de enumerador** área no cliente de la **colección** pestaña de la **Editor de bucles Foreach**.  
  
> [!IMPORTANT]  
>  Después de firmar y generar la interfaz de usuario personalizada e instalarla en la caché de ensamblados global tal y como se describe en [compilar, implementar y depurar objetos personalizados](../../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md), recuerde proporcionar el nombre completo de esta clase en el <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute.UITypeName%2A> propiedad de la <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute>.  
  
## <a name="coding-the-user-interface-control-class"></a>Codificar la clase Control de la interfaz de usuario  
  
### <a name="initializing-the-user-interface"></a>Inicializar la interfaz de usuario  
 Puede invalidar el método <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumeratorUI.Initialize%2A> para almacenar en memoria caché las referencias al objeto host y a las colecciones de administradores de conexión y variables definidas en el paquete.  
  
### <a name="setting-properties-on-the-user-interface-control"></a>Establecer las propiedades en el control de la interfaz de usuario  
 La clase de control de usuario, del que se deriva la clase de interfaz de usuario, está diseñada para su uso como un control compuesto para hospedar otros controles de formularios Windows Forms. Dado que esta clase hospeda otros controles, puede diseñar una interfaz de usuario personalizada arrastrando y quitando controles, organizándolos, estableciendo sus propiedades y respondiendo en tiempo de ejecución a los eventos como en cualquier aplicación de formularios Windows Forms.  
  
### <a name="saving-settings"></a>Guardar los valores  
 Puede invalidar el método <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumeratorUI.SaveSettings%2A> para copiar los valores seleccionados por el usuario de los controles en las propiedades del enumerador cuando el usuario cierra el editor.  
  
## <a name="see-also"></a>Vea también  
 [Crear un enumerador Foreach personalizado](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/creating-a-custom-foreach-enumerator.md)   
 [Codificar un enumerador Foreach personalizado](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/coding-a-custom-foreach-enumerator.md)  
  
  
