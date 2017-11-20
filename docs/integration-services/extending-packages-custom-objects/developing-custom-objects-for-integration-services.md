---
title: Desarrollar objetos personalizados para Integration Services | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-custom-objects
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom user interface [Integration Services]
- custom objects [Integration Services]
ms.assetid: ca1929a6-0ae6-47d7-b65f-08173b143720
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 6bbb7ccd5d65caa4b5c8cc8f28383b8100e09cd6
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="developing-custom-objects-for-integration-services"></a>Desarrollar objetos personalizados para Integration Services
  Cuando el flujo de control y los datos de flujo de objetos que se incluyen con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no cumplen completamente sus requisitos, puede desarrollar muchos tipos de objetos personalizados incluyendo:  
  
-   **Tareas personalizadas**.  
  
-   **Administradores de conexión personalizados.** Conexión a orígenes de datos externos que no son compatibles actualmente.  
  
-   **Proveedores de registro personalizados.** Eventos de paquete de registro en formatos que no son compatibles actualmente.  
  
-   **Enumeradores personalizados.** Admite iteración sobre un conjunto formatos de objetos o valores que no son compatibles actualmente.  
  
-   **Componentes de flujo de datos personalizados.** Se pueden configurar como orígenes, transformaciones o destinos.  
  
 El modelo de objetos [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] facilita este desarrollo personalizado con clases base que proporcionan un marco coherente y confiable para su implementación personalizada.  
  
 Si no tiene que reutilizar la funcionalidad personalizada por varios paquetes, la tarea Script y el componente de script le proporcionan toda la eficacia de un lenguaje de programación administrado con significativamente menos código de infraestructura para escribir. Para obtener más información, consulte [comparar soluciones de Scripting y objetos personalizados](../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md).  
  
## <a name="steps-in-developing-a-custom-object-for-integration-services"></a>Pasos para desarrollar un objeto personalizado para Integration Services  
 Cuando se desarrollar un objeto personalizado para su uso en [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], se desarrolla una biblioteca de clases (una DLL) que se cargará en tiempo de diseño y tiempo de ejecución por el Diseñador SSIS y por el tiempo de ejecución de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Los métodos más importantes que debe implementar no son métodos a los que llama desde su propio código, sino métodos que el tiempo de ejecución llama en los momentos adecuados para inicializar y validar su componente e invocar su funcionalidad.  
  
 A continuación figuran los pasos que se deben seguir para desarrollar un objeto personalizado:  
  
1.  Cree un nuevo proyecto de tipo biblioteca de clases en su lenguaje de programación administrado preferido.  
  
2.  Herede de la clase base adecuada, como se muestra en la tabla siguiente.  
  
3.  Aplique el atributo adecuado a su nueva clase, como se muestra en la tabla siguiente.  
  
4.  Invalide los métodos de la clase base tal y como se requiere, y escriba el código para la funcionalidad personalizada de su objeto.  
  
5.  Opcionalmente, construya una interfaz de usuario personalizada para su componente. Para facilitar la implementación, puede que desee desarrollar la interfaz de usuario como un proyecto independiente dentro de la misma solución y generarlo como un ensamblado independiente.  
  
6.  Si lo desea, mostrar un vínculo a ejemplos y al contenido de ayuda para el objeto personalizado, en el **cuadro de herramientas de SSIS**.  
  
7.  Compilar, implementar y depurar el nuevo objeto personalizado tal y como se describe en [compilar, implementar y depurar objetos personalizados](../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md).  
  
## <a name="base-classes-attributes-and-important-methods"></a>Clases base, atributos y métodos importantes  
 En esta tabla se proporciona una referencia sencilla de los elementos más importantes en el modelo de objetos [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para cada tipo de objeto personalizado que puede desarrollar.  
  
|Objeto personalizado|Clase base|Atributo|Métodos importantes|  
|-------------------|----------------|---------------|-----------------------|  
|Tarea|<xref:Microsoft.SqlServer.Dts.Runtime.Task>|<xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute>|<xref:Microsoft.SqlServer.Dts.Runtime.Task.Execute%2A>|  
|Administrador de conexiones|<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase>|<xref:Microsoft.SqlServer.Dts.Runtime.DtsConnectionAttribute>|<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.AcquireConnection%2A>, <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.ReleaseConnection%2A>|  
|Proveedor de registro|<xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase>|<xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute>|<xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.OpenLog%2A>, <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Log%2A>, <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.CloseLog%2A>|  
|Enumerador|<xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator>|<xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute>|<xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.GetEnumerator%2A>|  
|Componente de flujo de datos|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>|<xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A>, <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A>, <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A>|  
  
## <a name="providing-links-to-samples-and-help-content"></a>Proporcionar vínculos a ejemplos y al contenido de la Ayuda  
 Para mostrar un vínculo en el **cuadro de herramientas de SSIS** a ejemplos y al contenido de ayuda para un objeto personalizado escrito en código administrado, utilice las siguientes propiedades.  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.DTSPipelineComponentAttribute.SamplesTag%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.DTSPipelineComponentAttribute.HelpCollection%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.DTSPipelineComponentAttribute.HelpKeyword%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.DTSTaskAttribute.SamplesTag%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.DTSTaskAttribute.HelpCollection%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.DTSTaskAttribute.HelpKeyword%2A>  
  
 Para mostrar un vínculo a ejemplos y al contenido de la Ayuda para un objeto personalizado escrito en código nativo, agregue las entradas del archivo de script de Registro (.rgs) de SamplesTag, HelpKeyword y HelpCollection. A continuación se muestra un ejemplo.  
  
 `val HelpKeyword = s 'sql11.dts.designer.executepackagetask.F1'`  
  
 `val SamplesTag = s 'ExecutePackageTask'`  
  
## <a name="providing-a-custom-user-interface"></a>Proporcionar una interfaz de usuario personalizada  
 Para permitir a los usuarios de su objeto personalizado configurar sus propiedades, puede que tenga que desarrollar también una interfaz de usuario personalizada. En aquellos casos donde no se requiere una interfaz de usuario personalizada de forma estricta, puede que decida crear una para proporcionar una interfaz más fácil de comprender que el editor predeterminado.  
  
 En un proyecto o ensamblado personalizado de la interfaz de usuario, generalmente tiene dos clases: una clase que implementa una interfaz [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para las interfaces de usuario para el tipo específico de objeto personalizado y el formulario Windows Forms que se muestra para recopilar información del usuario. Las interfaces que implementa tienen solo unos cuantos métodos y una interfaz de usuario personalizada que no es difícil de desarrollar.  
  
> [!NOTE]  
>  Muchos [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] proveedores de registro tienen una interfaz de usuario personalizada que implementa <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsLogProviderUI> y reemplaza el **configuración** cuadro de texto con una lista desplegable filtrada de administradores de conexión disponibles. Sin embargo, las interfaces de usuario personalizadas para los proveedores de registro personalizados no se implementan en esta versión de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Especificar un valor para la propiedad <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute.UITypeName%2A> de <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute> no tiene ningún efecto.  
  
 La tabla siguiente proporciona una referencia sencilla para las interfaces que debe implementar al desarrollar una interfaz de usuario personalizada para cada tipo de objeto personalizado. También se explica lo que el usuario ve si decide no desarrollar una interfaz de usuario personalizada para el objeto, o si no puede vincular el objeto a su interfaz de usuario mediante la **UITypeName** propiedad en el atributo del objeto. Aunque el potente editor avanzado puede resultar satisfactorio para un componente de flujo de datos, la ventana Propiedades es una solución menos fácil de usar en tareas y administradores de conexión, y un enumerador ForEach personalizado no se puede configurar en absoluto sin un formulario personalizado.  
  
|Objeto personalizado|Clase base para la interfaz de usuario|Comportamiento de edición de valor predeterminado si no se proporciona ninguna interfaz de usuario personalizada|  
|-------------------|-----------------------------------|----------------------------------------------------------------------|  
|Tarea|<xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI>|Solo la ventana Propiedades|  
|Administrador de conexiones|<xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI>|Solo la ventana Propiedades|  
|Proveedor de registro|<xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsLogProviderUI><br /><br /> (No se implementa en [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)])|Cuadro de texto **configuración** columna|  
|Enumerador|<xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumeratorUI>|Solo la ventana Propiedades. El área del editor Configuración de enumeradores está vacía.|  
|Componente de flujo de datos|<xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI>|Editor avanzado|  
  
## <a name="external-resources"></a>Recursos externos  
  
-   Entrada de blog, [proceso de compilación de soluciones de Visual Studio proporcionan una advertencia acerca de la dependencia indirecta en el ensamblado de .NET Framework debido a referencias SSIS](http://go.microsoft.com/fwlink/?LinkId=215662), en blogs.msdn.com.  
  
## <a name="see-also"></a>Vea también  
 [Conservar objetos personalizados](../../integration-services/extending-packages-custom-objects/persisting-custom-objects.md)   
 [Generar, implementar y depurar objetos personalizados](../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)  
  
  

