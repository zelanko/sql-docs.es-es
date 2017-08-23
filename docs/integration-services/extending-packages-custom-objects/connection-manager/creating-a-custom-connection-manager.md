---
title: Crear un administrador de conexiones personalizado | Documentos de Microsoft
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
- custom connection managers [Integration Services], creating
ms.assetid: e83f8e02-ace4-42e0-b979-2f6be1460985
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2c617741134c19c012f487bc00263c2e4b071810
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="creating-a-custom-connection-manager"></a>Crear un administrador de conexiones personalizado
  Los pasos que debe seguir para crear un administrador de conexiones personalizado son similares a los pasos necesarios para crear cualquier otro objeto personalizado para [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]:  
  
-   Cree una clase nueva que herede de la clase base. Para un administrador de conexiones, la clase base es <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase>.  
  
-   Aplique el atributo que identifica el tipo de objeto para la clase. Para un administrador de conexiones, el atributo es <xref:Microsoft.SqlServer.Dts.Runtime.DtsConnectionAttribute>.  
  
-   Invalide la implementación de los métodos y las propiedades de la clase base. Para un administrador de conexiones, estos incluyen la propiedad <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.ConnectionString%2A> y los métodos <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.AcquireConnection%2A> y <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.ReleaseConnection%2A>.  
  
-   Si lo desea, desarrolle una interfaz de usuario personalizada. Para un administrador de conexiones, esto requiere una clase que implemente la interfaz <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI>.  
  
> [!NOTE]  
>  Muchas de las tareas, orígenes y destinos que se han incluido en [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] se usan únicamente con tipos específicos de administradores de conexiones integrados. Por consiguiente, estos ejemplos no se pueden probar con las tareas y componentes integrados.  
  
## <a name="getting-started-with-a-custom-connection-manager"></a>Introducción a un administrador de conexiones personalizado  
  
### <a name="creating-projects-and-classes"></a>Crear proyectos y clases  
 Dado que todos los administradores de conexiones administrados se derivan de la clase base <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase>, el primer paso para crear un administrador de conexiones personalizado consiste en crear un proyecto de bibliotecas de clases en el lenguaje de programación administrado que prefiera y, a continuación, crear una clase que herede de la clase base. En esta clase derivada, invalidará los métodos y propiedades de la clase base para implementar la funcionalidad personalizada.  
  
 En la misma solución, cree un segundo proyecto de bibliotecas de clases para la interfaz de usuario personalizada. Se recomienda usar un ensamblado independiente para la interfaz de usuario a fin de facilitar la implementación, ya que le permite actualizar y volver a implementar la tarea o su interfaz de usuario de forma independiente.  
  
 Configure ambos proyectos para firmar los ensamblados que se generarán en tiempo de compilación mediante un archivo de clave de nombre seguro.  
  
### <a name="applying-the-dtsconnection-attribute"></a>Aplicar el atributo DtsConnection  
 Aplique el atributo <xref:Microsoft.SqlServer.Dts.Runtime.DtsConnectionAttribute> a la clase que ha creado para identificarlo como un administrador de conexiones. Este atributo proporciona información en tiempo de diseño, como el nombre, la descripción y el tipo de conexión del administrador de conexiones. El <xref:Microsoft.SqlServer.Dts.Runtime.DtsConnectionAttribute.ConnectionType%2A> y **descripción** propiedades corresponden a la **tipo** y **descripción** las columnas mostradas en la **Agregar administrador de conexiones SSIS** cuadro de diálogo que se muestra al configurar las conexiones para un paquete en [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)].  
  
 Use la propiedad <xref:Microsoft.SqlServer.Dts.Runtime.DtsConnectionAttribute.UITypeName%2A> para vincular el administrador de conexiones a su interfaz de usuario personalizada. Para obtener el token de clave pública que se requiere para esta propiedad, puede usar **sn.exe -t** para mostrar el token de clave pública del archivo de par de claves (.snk) que se va a usar para firmar el ensamblado de la interfaz de usuario.  
  
```vb  
<DtsConnection(ConnectionType:="SQLVB", _  
  DisplayName:="SqlConnectionManager (VB)", _  
  Description:="Connection manager for Sql Server", _  
  UITypeName:="SqlConnMgrUIVB.SqlConnMgrUIVB,SqlConnMgrUIVB,Version=1.0.0.0,Culture=neutral,PublicKeyToken=<insert public key token here>")> _  
Public Class SqlConnMgrVB  
  Inherits ConnectionManagerBase  
  . . .  
End Class  
```  
  
```csharp  
[DtsConnection(ConnectionType = "SQLCS",  
  DisplayName = "SqlConnectionManager (CS)",  
  Description = "Connection manager for Sql Server",  
  UITypeName = "SqlConnMgrUICS.SqlConnMgrUICS,SqlConnMgrUICS,Version=1.0.0.0,Culture=neutral,PublicKeyToken=<insert public key token here>")]  
public class SqlConnMgrCS :  
ConnectionManagerBase  
{  
  . . .  
}  
```  
  
## <a name="building-deploying-and-debugging-a-custom-connection-manager"></a>Generar, implementar y depurar un administrador de conexiones personalizado  
 Los pasos para generar, implementar y depurar un administrador de conexiones personalizado en [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] son similares a los pasos necesarios en otros tipos de objetos personalizados. Para obtener más información, consulte [Building, Deploying and Debugging Custom Objects](../../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md).    
  
## <a name="see-also"></a>Vea también  
 [Codificar un administrador de conexiones personalizado](../../../integration-services/extending-packages-custom-objects/connection-manager/coding-a-custom-connection-manager.md)   
 [Desarrollar una interfaz de usuario para un administrador de conexiones personalizado](../../../integration-services/extending-packages-custom-objects/connection-manager/developing-a-user-interface-for-a-custom-connection-manager.md)  
  
  
