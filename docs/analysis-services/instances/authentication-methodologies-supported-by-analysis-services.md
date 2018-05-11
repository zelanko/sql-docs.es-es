---
title: Metodologías de autenticación admitidas por Analysis Services | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f7d1254e8bac0dd910468f1af1b4c0937fe0d23b
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="authentication-methodologies-supported-by-analysis-services"></a>Metodologías de autenticación admitidas por Analysis Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Las conexiones desde una aplicación cliente a una instancia de Analysis Services requieren la autenticación de Windows (integrada). Puede proporcionar una identidad de usuario de Windows mediante cualquiera de los métodos siguientes:  
  
-   NTLM  
  
-   Kerberos (vea [Configurar Analysis Services para la delegación restringida de Kerberos](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md))  
  
-   EffectiveUserName en la cadena de conexión  
  
-   Básica o Anónima (necesita la configuración para acceso HTTP)  
  
-   Credenciales almacenadas  
  
 Tenga en cuenta que la autenticación de notificaciones no se admite. No puede usar un token de notificaciones de Windows para tener acceso a Analysis Services. Las bibliotecas de cliente de Analysis Services solo funcionan con entidades de seguridad de Windows. Si la solución de BI incluye identidades de notificaciones, necesitará cuentas sombra de identidad de Windows para cada usuario o tendrá que usar credenciales almacenadas para tener acceso a los datos de Analysis Services.  
  
 Para obtener más información sobre BI y los flujos de autenticación de Analysis Services, vea [Autenticación y delegación de identidad de Microsoft BI](http://go.microsoft.com/fwlink/?LinkID=286576).  
  
##  <a name="bkmk_auth"></a> Descripción de las alternativas de autenticación  
 La conexión a una base de datos de Analysis Services requiere una identidad de usuario o grupo de Windows y permisos asociados. La identidad puede ser un inicio de sesión de propósito general usado por alguien que necesite consultar un informe, pero lo más probable es que incluya la identidad de usuarios individuales.  
  
 A menudo, los modelos multidimensionales o tabulares tendrán diferentes niveles de acceso a los datos, por objeto o bien dentro de los propios datos, en función de quién realice la solicitud. Para satisfacer este requisito, puede usar la autenticación NTLM, Kerberos, EffectiveUserName o Básica. Todas estas técnicas ofrecen distintas posibilidades de pasar diferentes identidades de usuario con cada conexión. Sin embargo, la mayoría de estas opciones están sujetas a la limitación de un solo salto. Solo Kerberos con delegación permite que la identidad de usuario original circule a través de conexiones entre varios equipos hasta un almacén de datos back-end en un servidor remoto.  
  
 **NTLM**  
  
 Para las conexiones que especifican `SSPI=Negotiate`, NTLM es el subsistema de autenticación de reserva que se usa cuando un controlador de dominio Kerberos no está disponible. En NTLM, cualquier usuario o aplicación cliente puede obtener acceso a un recurso del servidor siempre y cuando la solicitud sea una conexión directa del cliente al servidor, la persona que solicita la conexión tenga permiso en el recurso, y los equipos cliente y servidor se encuentren en el mismo dominio.  
  
 En las soluciones de varios niveles, la restricción de un solo salto de NLTM puede suponer un obstáculo importante. La identidad del usuario que realiza la solicitud se puede suplantar en exactamente un servidor remoto. Si la operación actual requiere que los servicios se ejecuten en varios equipos, deberá configurar la delegación restringida de Kerberos de modo que reutilice el token de seguridad en servidores back-end. Como alternativa puede usar las credenciales almacenadas o la autenticación básica para pasar nueva información de identidad a través de una conexión de un solo salto.  
  
 **Autenticación Kerberos y delegación restringida de Kerberos**  
  
 La autenticación Kerberos es la base de la seguridad integrada de Windows en los dominios de Active Directory. Como con NTLM, la suplantación en Kerberos está limitada a un solo salto, a no ser se que habilite la delegación.  
  
 Para admitir las conexiones de varios saltos, Kerberos proporciona la delegación restringida y no restringida, pero en la mayoría de los casos es preferible usar la delegación restringida porque es más segura. La delegación restringida permite que un servicio pueda pasar el token de seguridad de la identidad del usuario a un servicio de nivel inferior en un servidor remoto. Para las aplicaciones de varios niveles, la delegación de la identidad de un usuario desde un servidor de aplicación de nivel intermedio a un servidor back-end como Analysis Services es un proceso habitual. Por ejemplo, un modelo tabular o multidimensional que devuelve datos diferentes en función de la identidad del usuario necesitará la delegación de identidad de un servicio de nivel intermedio para evitar que el usuario tenga que volver a especificar las credenciales, u obtener credenciales de seguridad de algún otro modo.  
  
 Para la delegación restringida es necesario realizar una configuración adicional en Active Directory, donde los servicios tanto en el lado emisor como en el receptor de la solicitud están explícitamente autorizados para la delegación. Aunque inicialmente la configuración puede resultar costosa, una vez que el servicio está configurado las actualizaciones de contraseña se administran de forma independiente en Active Directory. No es necesario que actualice la información de cuenta almacenada en las aplicaciones, a diferencia de cuando se utiliza la opción de credenciales almacenadas que se describe más adelante.  
  
 Para obtener más información acerca de la configuración de Analysis Services para la delegación restringida, vea [Configure Analysis Services for Kerberos constrained delegation](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md).  
  
> [!NOTE]  
>  Windows Server 2012 admite la delegación restringida entre dominios. En cambio, para la configuración de la delegación restringida de Kerberos en dominios a niveles funcionales inferiores, como Windows Server 2008 o 2008 R2, es preciso que tanto los equipos cliente como servidor sean miembros del mismo dominio.  
  
 **EffectiveUserName**  
  
 EffectiveUserName es una propiedad de cadena de conexión usada para pasar la información de identidad a Analysis Services. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint la usa para registrar la actividad de los usuarios en los registros de uso. Excel Services y PerformancePoint Services la pueden usar para recuperar los datos empleados por los libros o paneles en SharePoint. También puede usarse en aplicaciones o scripts personalizados que ejecutan operaciones en una instancia de Analysis Services.  
  
 Para obtener más información acerca del uso de EffectiveUserName en SharePoint, vea [Usar EffectiveUserName de Analysis Services en SharePoint Server 2010](http://go.microsoft.com/fwlink/?LinkId=311905).  
  
 **Autenticación básica y usuario anónimo**  
  
 La autenticación básica ofrece una cuarta alternativa para la conexión a un servidor back-end como un usuario específico. Con la autenticación básica, el nombre de usuario y la contraseña de Windows se pasan a la cadena de conexión, que incluye requisitos de cifrado de cable adicional para garantizar que la información confidencial está protegida durante el envío. Una ventaja importante que ofrece la autenticación básica es que la solicitud de autenticación puede cruzar los límites de los dominios.  
  
 Para la autenticación Anónima, puede establecer la identidad de usuario anónima en una cuenta de usuario de Windows concreta (IUSR_GUEST de forma predeterminada) o en una identidad de grupo de aplicaciones. La cuenta de usuario anónima se usará en la conexión de Analysis Services y debe tener permisos de acceso a datos en la instancia de Analysis Services. Si utiliza este método, en la conexión solo se utiliza la identidad de usuario asociada a la cuenta anónima. Si su aplicación precisa de una administración de identidades adicional, deberá elegir uno de los otros métodos, o bien complementar la aplicación con una solución de administración de identidades propia.  
  
 Básica y Anónima solo están disponibles al configurar Analysis Services para acceso HTTP con el uso de IIS y msmdpump.dll para establecer la conexión. Para obtener más información, vea [Configurar el acceso HTTP a Analysis Services en Internet Information Services &#40;IIS&#41; 8.0](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md).  
  
 **Stored Credentials**  
  
 La mayoría de servicios de aplicación de nivel intermedio incluyen la funcionalidad para almacenar un nombre de usuario y una contraseña que posteriormente se usarán para recuperar datos de un almacén de datos de nivel inferior, como Analysis Services o el motor relacional de SQL Server. En sí, las credenciales almacenadas ofrecen una quinta alternativa para recuperar datos. Entre las limitaciones inherentes a este método se incluye la sobrecarga de mantenimiento asociada con la actualización de los nombres de usuario y las contraseñas, y el uso de una sola identidad en la conexión. Si su solución precisa de la identidad del autor de la llamada original, las credenciales almacenadas no serían una alternativa viable.  
  
 Para obtener más información sobre las credenciales almacenadas, vea [Crear, modificar y eliminar orígenes de datos compartidos &#40;SSRS&#41;](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md) y [Usar Servicios de Excel con el Servicio de almacenamiento seguro en SharePoint Server 2013](http://go.microsoft.com/fwlink/?LinkID=309869).  
  
## <a name="see-also"></a>Vea también  
 [Usar la suplantación con seguridad de transporte](http://go.microsoft.com/fwlink/?LinkId=311727)   
 [Configurar el acceso HTTP a Analysis Services en Internet Information Services &#40;IIS&#41; 8.0](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)   
 [Configurar Analysis Services para la delegación restringida de Kerberos](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md)   
 [Registro de SPN para una instancia de Analysis Services](../../analysis-services/instances/spn-registration-for-an-analysis-services-instance.md)   
 [Conectar a Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md)  
  
  
