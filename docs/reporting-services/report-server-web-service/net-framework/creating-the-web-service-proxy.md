---
title: Crear el Proxy de servicio Web | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Report Server Web service, proxies
- proxies [Reporting Services]
- XML Web service [Reporting Services], proxies
- Web service [Reporting Services], proxies
- Web references [Reporting Services]
ms.assetid: b1217843-8d3d-49f3-a0d2-d35b0db5b2df
caps.latest.revision: 44
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 727d9ccd8cd1e40d89cfe74291edae92988b407c
ms.openlocfilehash: 1c39d81ec9a1d2cd24f01b9dccfed13e8560a770
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="creating-the-web-service-proxy"></a>Crear al Proxy de servicio Web
  Un cliente y un servicio web pueden comunicarse utilizando mensajes SOAP, que encapsulan los parámetros de entrada y salida como XML. Una clase de proxy asigna los parámetros a los elementos XML y, a continuación, envía los mensajes SOAP a través de una red. De esta manera, la clase de proxy le evita tener que comunicarse con el servicio web en el nivel SOAP y le permite invocar a los métodos de servicio web en cualquier entorno de desarrollo que admita SOAP y proxys de servicio web.  
  
 Hay dos maneras de agregar una clase de proxy para el proyecto de desarrollo con el [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]: con la herramienta WSDL en el [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]y agregando una referencia Web en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]. En las secciones siguientes se explica esta cuestión con mayor detalle.  
  
## <a name="adding-the-proxy-using-the-wsdl-tool"></a>Agregar el proxy mediante la herramienta WSDL  
 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] SDK incluye la herramienta Lenguaje de descripción de servicios web (Wsdl.exe), que permite generar un proxy de servicio web para usarse en el entorno de desarrollo de [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]. La manera más común para crear un proxy de cliente en los lenguajes que admiten servicios Web (actualmente C# y [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]) consiste en utilizar la herramienta WSDL.  
  
 **Para agregar una clase de proxy a un proyecto utilizando Wsdl.exe**  
  
1.  Desde un símbolo del sistema, utilice Wsdl.exe para crear una clase de proxy, especificando, como mínimo, la dirección URL del servicio web del servidor de informes.  
  
     Por ejemplo, la siguiente instrucción del símbolo del sistema especifica una dirección URL para el extremo de administración del servicio web del servidor de informes:  
  
    ```  
    wsdl /language:CS /n:"Microsoft.SqlServer.ReportingServices2010" http://<Server Name>/reportserver/reportservice2010.asmx?wsdl  
    ```  
  
     La herramienta WSDL acepta varios argumentos de símbolo del sistema para generar un proxy. El ejemplo anterior especifica el lenguaje C# y un espacio de nombres sugerido para utilizar en el proxy (para evitar el conflicto de nombres si se usa más de un extremo de servicios web), y genera un archivo de C# denominado ReportingService2010.cs. Si el ejemplo hubiera especificado [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)], el ejemplo habría generado un archivo de proxy con el nombre ReportingService2010.vb. Este archivo se crea en el directorio desde el que se ejecuta el comando.  
  
2.  Compile la clase de proxy en un archivo de ensamblado (con la extensión .dll) y haga referencia a él en el proyecto o agregue la clase como un elemento de proyecto.  
  
    > [!NOTE]  
    >  Al agregar manualmente una clase de proxy al proyecto, tiene que agregar una referencia al archivo System.Web.Services.dll. Si agrega el proxy utilizando una referencia web en Visual Studio .NET, la referencia se crea automáticamente. Para obtener más información, vea "Agregar el proxy usando una referencia web en Visual Studio" más adelante en este tema.  
  
     Después de agregar la clase de proxy como un elemento al proyecto, el archivo asociado aparece en el Explorador de soluciones.  
  
3.  Para llamar al servicio mediante programación, cree una instancia de la clase de proxy.  
  
     El ejemplo de código siguiente muestra la sintaxis para crear una instancia de la clase de proxy <xref:ReportService2010.ReportingService2010> en un proyecto:  
  
```vb  
Dim service As New ReportingService2010()  
```  
  
```csharp  
ReportingService2010 service = new ReportingService2010();  
  
```  
  
 Para obtener más información sobre la herramienta Wsdl.exe, incluida su sintaxis completa, vea "Herramienta Lenguaje de descripción de servicios web" en la documentación de [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] SDK. Para obtener una explicación completa de los proxys del servicio web, vea "Crear un proxy de servicio web XML" en la documentación de [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] SDK.  
  
## <a name="adding-the-proxy-using-a-web-reference-in-visual-studio"></a>Agregar el proxy usando una referencia web en Visual Studio  
 Una referencia web permite a un proyecto usar uno o más servicios web. [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] permite a los usuarios agregar referencias de servicio web a los proyectos siguiendo unos pasos simples.  
  
 **Para agregar una referencia Web a un proyecto**  
  
1.  En **el Explorador de soluciones**, seleccione el proyecto que consumirá el servicio Web.  
  
2.  En el **proyecto** menú, haga clic en **Agregar referencia Web**.  
  
     El **Agregar referencia Web** abre el cuadro de diálogo.  
  
3.  En el **dirección URL** , escriba la ruta de acceso completa al servicio Web del servidor de informes.  
  
     Una dirección URL simplificada para el extremo de ejecución de informes del servicio web del servidor de informes podría ser similar a la siguiente:  
  
    ```  
    http://<Server Name>/reportserver/reportexecution2005.asmx  
    ```  
  
     La dirección URL contiene el dominio en el que se implementa el servicio web del servidor de informes, el nombre de la carpeta que contiene el servicio y el nombre del archivo de detección para el servicio. Para obtener una descripción completa de los distintos elementos de la dirección URL, vea [acceder a la API SOAP](../../../reporting-services/report-server-web-service/accessing-the-soap-api.md).  
  
     Una descripción de los métodos y propiedades proporcionada por el servicio web aparece en el panel Explorador a la izquierda.  
  
    > [!NOTE]  
    >  Para obtener más información acerca de los elementos asociados con el servicio Web del servidor de informes, consulte [métodos de servicio Web de servidor de informes](../../../reporting-services/report-server-web-service/methods/report-server-web-service-methods.md).  
  
4.  Compruebe que su proyecto puede utilizar el servicio web del servidor de informes y que tiene el permiso adecuado para tener acceso al servidor de informes.  
  
5.  En el **nombre de referencia Web** , a continuación, escriba un nombre que va a utilizar en el código para tener acceso el servicio Web del servidor de informes mediante programación.  
  
6.  Seleccione el **Agregar referencia** botón para crear una referencia en la aplicación para el servicio Web.  
  
     La nueva referencia aparece en **el Explorador de soluciones** bajo el nodo referencias Web para el proyecto activo, denominado tal como se especifica en el **nombre de referencia Web** campo.  
  
7.  En **el Explorador de soluciones**, expanda la carpeta referencias Web para tener en cuenta el espacio de nombres para las clases de referencia Web que están disponibles para los elementos de su proyecto.  
  
     Después de agregar una referencia Web al proyecto, los archivos asociados se muestran en una carpeta dentro de la carpeta referencias Web de **el Explorador de soluciones**.  
  
 Después de agregar la referencia web, utilice la sintaxis siguiente para crear una instancia de la clase de proxy:  
  
```vb  
Dim rs As New myNamespace.myReferenceName.ReportExecutionService()  
rs.Url = "http://<Server Name>/reportserver/reportexecution2005.asmx?wsdl"  
rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
```  
  
```csharp  
myNamespace.myReferenceName.ReportExecutionService rs = new myNamespace.myReferenceName.ReportExecutionService();  
rs.Url = "http://<Server Name>/reportserver/reportexecution2005.asmx?wsdl"  
rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
  
```  
  
 También puede agregar un **con** (**importación** en [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]) la directiva a la referencia de servicio Web del servidor de informes. Si utiliza esta directiva, no es necesario utilizar nombres completos para los tipos en el espacio de nombres. En ello, agregue el siguiente código al archivo:  
  
```vb  
Import myNamespace.myReferenceName  
```  
  
```csharp  
using myNamespace.myReferenceName;  
```  
  
## <a name="see-also"></a>Vea también  
 [Servicio Web de servidor de informes](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [Creación de aplicaciones con el servicio Web y .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Referencia técnica de &#40; SSRS &#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  
