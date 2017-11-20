---
title: Crear un enumerador Foreach personalizado | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
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
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom foreach enumerators [Integration Services], creating
ms.assetid: 050e8455-2ed0-4b6d-b3ea-4e80e6c28487
caps.latest.revision: 53
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: f2f852ff319554d0b863fd06d790c2e5e9bf2d59
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="creating-a-custom-foreach-enumerator"></a>Crear un enumerador foreach personalizado
  Los pasos necesarios para crear un enumerador foreach personalizado son similares a los pasos para crear cualquier otro objeto personalizado para [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]:  
  
-   Cree una clase nueva que herede de la clase base. Para un enumerador foreach, la clase base es <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator>.  
  
-   Aplique el atributo que identifica el tipo de objeto para la clase. Para un enumerador foreach, el atributo es <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute>.  
  
-   Reemplace la implementación de métodos y propiedades de la clase base. Para un enumerador foreach, el más importante es el método <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.GetEnumerator%2A>.  
  
-   Si lo desea, desarrolle una interfaz de usuario personalizada. Para un enumerador foreach, esto requiere una clase que implemente la interfaz <xref:Microsoft.SqlServer.Dts.Runtime.IDTSForEachEnumeratorUI>.  
  
 El contenedor <xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop> hospeda un enumerador personalizado. En tiempo de ejecución, el contenedor <xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop> llama al método <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.GetEnumerator%2A> del enumerador personalizado. El enumerador personalizado devuelve un objeto que implementa el **IEnumerable** interfaz, como un **ArrayList**. A continuación, <xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop> establece una iteración en cada elemento de la colección, proporciona el valor del elemento actual al flujo de control a través de una variable definida por el usuario y ejecuta el flujo de control en el contenedor.  
  
## <a name="getting-started-with-a-custom-foreach-enumerator"></a>Introducción a los enumeradores Foreach personalizados  
  
### <a name="creating-projects-and-classes"></a>Crear proyectos y clases  
 Dado que todos los enumeradores foreach administrados se derivan de la clase base <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator>, el primer paso al crear un enumerador foreach personalizado consiste en crear un proyecto de bibliotecas de clases en el lenguaje de programación administrado que prefiera y crear una clase que herede de la clase base. En esta clase derivada se invalidarán los métodos y las propiedades de la clase base para implementar la funcionalidad personalizada.  
  
 En la misma solución, cree un segundo proyecto de bibliotecas de clases para la interfaz de usuario personalizada. Se recomienda utilizar un ensamblado independiente para la interfaz de usuario a fin de facilitar la implementación, ya que le permite actualizar y volver a implementar el enumerador foreach o su interfaz de usuario de forma independiente.  
  
 Configure ambos proyectos para firmar los ensamblados que se generarán en tiempo de compilación mediante un archivo de clave de nombre seguro.  
  
### <a name="applying-the-dtsforeachenumerator-attribute"></a>Aplicar el atributo DtsForEachEnumerator  
 Aplique el atributo <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute> a la clase que ha creado para identificarla como enumerador foreach. Este atributo proporciona información en tiempo de diseño, como el nombre y la descripción del enumerador foreach. El **nombre** propiedad aparece en la lista desplegable de enumeradores disponibles en la **colección** pestaña de la **Editor de bucles Foreach** cuadro de diálogo.  
  
 Utilice la propiedad <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute.UITypeName%2A> para vincular el enumerador foreach a su interfaz de usuario personalizada. Para obtener el token de clave pública que se requiere para esta propiedad, puede usar **sn.exe -t** para mostrar el token de clave pública del archivo de par de claves (.snk) que se va a usar para firmar el ensamblado de la interfaz de usuario.  
  
```vb  
Imports System  
Imports Microsoft.SqlServer.Dts.Runtime  
Namespace Microsoft.Samples.SqlServer.Dts  
    <DtsForEachEnumerator(DisplayName = "MyEnumerator", Description="A sample custom enumerator", UITypeName="FullyQualifiedTypeName,AssemblyName,Version=1.00.000.00,Culture=Neutral,PublicKeyToken=<publickeytoken>")> _   
    Public Class MyEnumerator  
     Inherits ForEachEnumerator  
        'Insert code here.  
    End Class  
End Namespace  
```  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
namespace Microsoft.Samples.SqlServer.Dts  
{  
    [DtsForEachEnumerator( DisplayName = "MyEnumerator", Description="A sample custom enumerator", UITypeName="FullyQualifiedTypeName,AssemblyName,Version=1.00.000.00,Culture=Neutral,PublicKeyToken=<publickeytoken>")]  
    public class MyEnumerator : ForEachEnumerator  
    {  
        //Insert code here.  
    }  
}  
```  
  
## <a name="building-deploying-and-debugging-a-custom-enumerator"></a>Generar, implementar y depurar un enumerador personalizado  
 Los pasos para generar, implementar y depurar un enumerador foreach personalizado en [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] son muy similares a los pasos requeridos para otros tipos de objetos personalizados. Para obtener más información, consulte [Building, Deploying and Debugging Custom Objects](../../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md).  
  
## <a name="see-also"></a>Vea también  
 [Codificar un enumerador Foreach personalizado](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/coding-a-custom-foreach-enumerator.md)   
 [Desarrollar una interfaz de usuario para un enumerador ForEach personalizado](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/developing-a-user-interface-for-a-custom-foreach-enumerator.md)  
  
  

