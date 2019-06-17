---
title: Crear un enumerador Para cada uno personalizado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom foreach enumerators [Integration Services], creating
ms.assetid: 050e8455-2ed0-4b6d-b3ea-4e80e6c28487
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 49455bf9a5138d539a13ed241a24ab5d720c7f43
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62896085"
---
# <a name="creating-a-custom-foreach-enumerator"></a>Crear un enumerador foreach personalizado
  Los pasos necesarios para crear un enumerador foreach personalizado son similares a los pasos para crear cualquier otro objeto personalizado para [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]:  
  
-   Cree una clase nueva que herede de la clase base. Para un enumerador foreach, la clase base es <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator>.  
  
-   Aplique el atributo que identifica el tipo de objeto para la clase. Para un enumerador foreach, el atributo es <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute>.  
  
-   Invalide la implementación de los métodos y las propiedades de la clase base. Para un enumerador foreach, el más importante es el método <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.GetEnumerator%2A>.  
  
-   Si lo desea, desarrolle una interfaz de usuario personalizada. Para un enumerador foreach, esto requiere una clase que implemente la interfaz <xref:Microsoft.SqlServer.Dts.Runtime.IDTSForEachEnumeratorUI>.  
  
 El contenedor <xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop> hospeda un enumerador personalizado. En tiempo de ejecución, el contenedor <xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop> llama al método <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.GetEnumerator%2A> del enumerador personalizado. El enumerador personalizado devuelve un objeto que implementa la interfaz `IEnumerable`, por ejemplo, un objeto `ArrayList`. A continuación, <xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop> establece una iteración en cada elemento de la colección, proporciona el valor del elemento actual al flujo de control a través de una variable definida por el usuario y ejecuta el flujo de control en el contenedor.  
  
## <a name="getting-started-with-a-custom-foreach-enumerator"></a>Introducción a los enumeradores Foreach personalizados  
  
### <a name="creating-projects-and-classes"></a>Crear proyectos y clases  
 Dado que todos los enumeradores foreach administrados se derivan de la clase base <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator>, el primer paso al crear un enumerador foreach personalizado consiste en crear un proyecto de bibliotecas de clases en el lenguaje de programación administrado que prefiera y crear una clase que herede de la clase base. En esta clase derivada se invalidarán los métodos y las propiedades de la clase base para implementar la funcionalidad personalizada.  
  
 En la misma solución, cree un segundo proyecto de bibliotecas de clases para la interfaz de usuario personalizada. Se recomienda utilizar un ensamblado independiente para la interfaz de usuario a fin de facilitar la implementación, ya que le permite actualizar y volver a implementar el enumerador foreach o su interfaz de usuario de forma independiente.  
  
 Configure ambos proyectos para firmar los ensamblados que se generarán en tiempo de compilación mediante un archivo de clave de nombre seguro.  
  
### <a name="applying-the-dtsforeachenumerator-attribute"></a>Aplicar el atributo DtsForEachEnumerator  
 Aplique el atributo <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute> a la clase que ha creado para identificarla como enumerador foreach. Este atributo proporciona información en tiempo de diseño, como el nombre y la descripción del enumerador foreach. El `Name` propiedad aparece en la lista desplegable de enumeradores disponibles en el **colección** pestaña de la **Editor de bucles Foreach** cuadro de diálogo.  
  
 Utilice la propiedad <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute.UITypeName%2A> para vincular el enumerador foreach a su interfaz de usuario personalizada. Para obtener el token de clave pública necesario para esta propiedad, puede usar **sn.exe -t** con el fin de mostrar el token de clave pública del archivo de pares de claves (.snk) que quiere usar para firmar el ensamblado de la interfaz de usuario.  
  
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
 Los pasos para generar, implementar y depurar un enumerador foreach personalizado en [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] son muy similares a los pasos requeridos para otros tipos de objetos personalizados. Para obtener más información, consulte [Generar, implementar y depurar objetos personalizados](../building-deploying-and-debugging-custom-objects.md).  
  
![Icono de Integration Services (pequeño)](../../media/dts-16.gif "icono de Integration Services (pequeño)")**mantenerse actualizado con Integration Services**<br /> Para obtener las descargas, artículos, ejemplos y vídeos más recientes de Microsoft, así como soluciones seleccionadas de la comunidad, visite la página de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] en MSDN:<br /><br /> [Visite la página de Integration Services en MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para recibir notificaciones automáticas de estas actualizaciones, suscríbase a las fuentes RSS disponibles en la página.  
  
## <a name="see-also"></a>Vea también  
 [Programar un enumerador Para cada uno personalizado](coding-a-custom-foreach-enumerator.md)   
 [Desarrollar una interfaz de usuario para un enumerador ForEach personalizado](developing-a-user-interface-for-a-custom-foreach-enumerator.md)  
  
  
