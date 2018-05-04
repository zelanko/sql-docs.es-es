---
title: Power Pivot Authentication and Authorization | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ppvt-sharepoint
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 710db3b55eb8e3bd1e885dfd71e2bde15360092c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="power-pivot-authentication-and-authorization"></a>Autenticación y autorización de PowerPivot
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Una implementación de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint que se ejecuta dentro de una granja de servidores de SharePoint 2010 usa el subsistema de autenticación y el modelo de autorización que proporcionan los servidores de SharePoint. La infraestructura de seguridad de SharePoint se extiende al contenido y a las operaciones de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , ya que todo el contenido relacionado con [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]está almacenado en bases de datos de contenido de SharePoint y todas las operaciones relacionadas con [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]las realizan los servicios compartidos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en la granja. Los usuarios que solicitan un libro que contenga los datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] se autentican con una identidad de usuario de SharePoint que se basa en su identidad de usuario de Windows. Los permisos para ver el libro determinan si la solicitud se concede o se deniega.  
  
 Dado que para el análisis de los datos de autoservicio se requiere la integración con Excel Services, la protección de un servidor de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] requiere que también se conozca la seguridad de Excel Services. Cuando un usuario consulta una tabla dinámica que tiene una conexión de datos a datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , Excel Services reenvía una solicitud de conexión de datos a un servidor de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] de la granja para cargar los datos. Esta interacción entre los servidores requiere saber cómo establecer una configuración de seguridad para ambos.  
  
 Haga clic en los siguientes vínculos para leer secciones concretas de este tema:  
  
 [Autenticación de Windows mediante el inicio de sesión en modo clásico](../../analysis-services/power-pivot-sharepoint/power-pivot-authentication-and-authorization.md#bkmk_auth)  
  
 [Operaciones de PowerPivot que requieren la autorización del usuario](#UserConnections)  
  
 [Permisos de SharePoint para el acceso a datos PowerPivot](#Permissions)  
  
 [Consideraciones de seguridad de Excel Services para los libros PowerPivot](#excel)  
  
##  <a name="bkmk_auth"></a> Autenticación de Windows mediante el inicio de sesión en modo clásico  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint admite un conjunto reducido de las opciones de autenticación disponibles en SharePoint. De las opciones de autenticación disponibles, solo se admite la autenticación de Windows para una implementación de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint. Además, la aplicación web a través de la que se produce el inicio de sesión debe estar configurada para el modo clásico.  
  
 Se requiere la autenticación de Windows porque el motor de datos de Analysis Services de una implementación de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint solo admite este tipo de autenticación. Excel Services establece conexiones con Analysis Services a través del proveedor OLE DB MSOLAP mediante una identidad de usuario de Windows que se ha autenticado a través de NTLM o del protocolo Kerberos.  
  
 El segundo requisito, la autenticación en modo clásico en la aplicación web, es necesario para asegurarse de que el servicio web [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] funciona. El servicio web es un componente que se ejecuta en un servidor front-end web y que proporciona redireccionamiento HTTP a un servidor [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint de la granja. Aunque el servicio web dispone de notificaciones para las comunicaciones entre servicios, no cuenta con ellas para las solicitudes de conexión de datos que redirige a un servicio compartido [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] de la granja. Las solicitudes para cargar los datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] solo se admiten en las conexiones autenticadas que proceden de IIS y usan una identidad de Windows. El inicio de sesión en modo clásico en la aplicación web es lo que permite una conexión correcta desde el servicio web [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] a los servicios compartidos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en la granja.  
  
 Aunque el inicio de sesión en modo clásico no es necesario en el escenario de acceso a datos más frecuente (cuando los datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] se extraen del mismo libro de Excel que los representa), no intente usar [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint con aplicaciones web de SharePoint configuradas para usar otros proveedores de autenticación. Si lo hace, se producirá un error de conexión cada vez que los usuarios traten de conectarse con libros [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] como origen de datos externo.  
  
 Sin el inicio de sesión en modo clásico, los siguientes tipos de solicitudes administradas por el servicio web de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] generarán un error:  
  
-   Cualquier solicitud de datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] que se origine desde fuera de la granja (por ejemplo, la creación de un informe en el Diseñador de informes o en el Generador de informes, donde el origen de datos es una URL de SharePoint que apunta a un libro [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ).  
  
-   Las solicitudes originadas en la granja desde una aplicación cliente o informes que usen un libro [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] como origen de datos externo (por ejemplo, crear un libro en la aplicación de escritorio de Excel, usando como origen de datos un segundo libro de Excel publicado que contiene datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ).  
  
### <a name="how-to-check-the-authentication-provider-for-your-application"></a>Comprobar el proveedor de autenticación para la aplicación  
 Cuando cree nuevas aplicaciones web, asegúrese de seleccionar la opción **Modo clásico de autenticación** en la página Crear nueva aplicación web.  
  
 En el caso de aplicaciones web existentes, use las siguientes instrucciones para comprobar que la aplicación web está configurada para usar la autenticación de Windows.  
  
1.  En Administración central, en Administración de aplicaciones, haga clic en **Administrar las aplicaciones web**.  
  
2.  Seleccione la aplicación web.  
  
3.  Haga clic en **Proveedores de autenticación**.  
  
4.  Compruebe que tiene un proveedor para cada zona, y que la zona predeterminada está establecida en Windows.  
  
##  <a name="UserConnections"></a> Operaciones de PowerPivot que requieren la autorización del usuario  
 La autorización de SharePoint se usa exclusivamente para todos los niveles de acceso al procesamiento de datos y las consultas de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
 No se admite el modelo de autorización basada en roles de Analysis Services. No hay ninguna autorización basada en roles para los datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en el nivel de celda, fila o tabla. No puede proteger partes diferentes del libro para conceder o denegar el acceso a la información confidencial que contiene para usuarios concretos. Los datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] incrustados están completamente disponibles para los usuarios que tienen permisos para ver el libro de Excel en una biblioteca de SharePoint.  
  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint suplantará a un usuario de SharePoint en los casos siguientes:  
  
-   Consultas a tablas dinámicas o gráficos dinámicos que tengan conexiones de datos a una base de datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , donde una aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] establece las conexiones en nombre de un usuario a una instancia de servicio compartido [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] concreta que procesa los datos.  
  
-   La carga de datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] de la memoria caché o de una biblioteca, si los datos no están disponibles de otra forma. Si se realiza una solicitud de conexión de datos para datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] que aún no está cargados en el sistema, la instancia de [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] usará la identidad del usuario de SharePoint para recuperar el origen de datos de una biblioteca de contenido y cargarlo en la memoria.  
  
-   Las operaciones de actualización de datos que guardan una copia actualizada del origen de datos al libro en una biblioteca de contenido. En este caso, se realiza un registro real de la operación utilizando el nombre de usuario y la contraseña que se recuperan de una aplicación de destino en el Servicio de almacenamiento seguro. Las credenciales pueden ser la cuenta de actualización de datos desatendida de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] o las credenciales que se almacenaron con la programación de actualización de datos al crearse. Para obtener más información, consulte [Configurar las credenciales almacenadas para la actualización de datos PowerPivot (PowerPivot para SharePoint)](http://msdn.microsoft.com/en-us/987eff0f-bcfe-4bbd-81e0-9aca993a2a75) y [Configurar la cuenta de actualización de datos desatendida de PowerPivot (PowerPivot para SharePoint)](http://msdn.microsoft.com/en-us/81401eac-c619-4fad-ad3e-599e7a6f8493).  
  
##  <a name="Permissions"></a> Permisos de SharePoint para el acceso a datos PowerPivot  
 La publicación, administración y protección de un libro [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] únicamente se admite a través de la integración de SharePoint. Los servidores de SharePoint proporcionan subsistemas de autenticación y autorización que se aseguran de que se produce un acceso legítimo a los datos. No hay ningún escenario admitido para implementar de forma segura un libro [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] fuera de una granja de SharePoint.  
  
 El acceso de usuario a los datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] del servidor es de solo lectura mediante permisos de visualización o superiores. Los permisos de contribución permiten agregar y modificar el archivo. Las modificaciones en los datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] requieren la descarga del libro a una aplicación de escritorio de Excel que tenga instalado [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para Excel. Los permisos de contribución en el archivo determinarán si el usuario puede descargar el archivo localmente y guardar los cambios de nuevo en SharePoint.  
  
 Por tanto, los niveles de permisos de contribución y solo visualización definen el conjunto vigente de permisos para el acceso de los usuarios a los datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Otros niveles de permisos funcionan hasta el punto en que tienen los mismos permisos que Contribuir y Solo ver (por ejemplo, dado que Lectura incluye los permisos Solo ver, un usuario al que se le asigne Lectura tendrá el mismo acceso que otro con el permiso Solo ver).  
  
 En la siguiente tabla se resumen los niveles de permisos que determinan el acceso a los datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] y operaciones del servidor:  
  
|Nivel del permiso|Permite estas tareas|  
|----------------------|------------------------|  
|Administrador de granja o de servicio|Instalar, habilitar y configurar servicios y aplicaciones.<br /><br /> Usar el panel de administración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] y ver informes administrativos.|  
|Control total|Activar la integración de características de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en el nivel de colección de sitios.<br /><br /> Crear una biblioteca de la galería de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .<br /><br /> Crear una biblioteca de fuentes de distribución de datos.|  
|Contribuir|Agregar, editar, eliminar y descargar libros [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .<br /><br /> Configurar actualización de datos.<br /><br /> Crear nuevos libros e informes basados en libros [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en un sitio de SharePoint.<br /><br /> Crear documentos de servicio de datos en una biblioteca de fuentes de distribución de datos.|  
|Lectura|Acceder a libros [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] como origen de datos externo, donde la URL del libro se escribe explícitamente en un cuadro de diálogo de conexión (por ejemplo, en el Asistente para conexión de datos de Excel).|  
|Solo ver|Ver libros [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .<br /><br /> Ver el historial de la actualización de datos.<br /><br /> Conectarse con un libro local a un libro [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en un sitio de SharePoint, para cambiar sus datos de otras formas.<br /><br /> Descargue una instantánea del libro. La instantánea es una copia estática de los datos, segmentaciones de datos, filtros, fórmulas ni conexiones de datos. El contenido de la instantánea es parecido al que se obtiene al copiar los valores de las celdas de la ventana del explorador.|  
  
##  <a name="excel"></a> Consideraciones de seguridad de Excel Services para los libros PowerPivot  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] El procesamiento de consultas en el lado servidor está ligado estrechamente a los servicios de Excel. La integración de productos comienza en el nivel de documento, donde los libros [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] son archivos de libro de Excel (.xlsx) que contienen datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] o hacen referencia a ellos. No hay ninguna extensión de archivo independiente para un libro [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
 Cuando un libro [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] se abre en un sitio de SharePoint, Excel Services lee las cadenas de conexión de datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] incrustadas y reenvía la solicitud al proveedor OLE DB de Analysis Services de SQL Server local. Después, el proveedor pasa la información de conexión a un servidor de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en la granja. Para que la solicitud fluya uniformemente entre los dos servidores, Excel Services se debe configurar para usar valores que son requeridos por [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint.  
  
 En Excel Services, la configuración relativa a la seguridad se especifica en las ubicaciones confiables, proveedores de datos confiables y bibliotecas de conexiones de datos confiables. En la siguiente tabla se describen los valores que habilitan o mejoran el acceso a datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Si no aparece aquí un valor, no tiene ningún efecto en las conexiones con el servidor de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Para obtener instrucciones sobre cómo especificar estos valores paso a paso, consulte la sección "Paso 4: Habilitar Excel Services" en [Configuración inicial (PowerPivot para SharePoint)](http://msdn.microsoft.com/en-us/3a0ec2eb-017a-40db-b8d4-8aa8f4cdc146).  
  
> [!NOTE]  
>  La mayoría de la configuración relacionada con la seguridad se aplica a las ubicaciones confiables. Si desea conservar los valores predeterminados o usar valores diferentes para sitios distintos, puede crear una ubicación confiable adicional para sitios que contienen datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] y, después, configurar los siguientes valores solo para ese sitio. Para más información, vea [Crear una ubicación de confianza para los sitios PowerPivot en Administración central](../../analysis-services/power-pivot-sharepoint/create-a-trusted-location-for-power-pivot-sites-in-central-administration.md).  
  
|Área|Configuración|Description|  
|----------|-------------|-----------------|  
|Aplicación web|Proveedor de autenticación de Windows|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] convierte un token de notificación que obtiene de Excel Services en una identidad de usuario de Windows. Cualquier aplicación web que use Excel Services como un recurso se debe configurar para usar el proveedor de autenticación de Windows.|  
|Ubicación confiable|Tipo de ubicación|Este valor debe estar establecido en **Microsoft SharePoint Foundation**. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] recuperan una copia del archivo .xlsx y la cargan en un servidor de Analysis Services en la granja. El servidor solo puede recuperar archivos .xlsx de una biblioteca de contenidos.|  
||Permitir datos externos|Este valor debe estar establecido en **Bibliotecas de conexiones de datos de confianza e incrustadas**. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] contienen conexiones de datos incrustadas. Si deniega las conexiones incrustadas, los usuarios pueden ver la memoria caché de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , pero no podrán utilizar los datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .|  
||Avisar al actualizar|Este valor debería estar deshabilitado si está usando la galería de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para almacenar libros e informes. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] incluye una característica de vista previa de documentos que funciona mejor si están desactivadas las opciones de actualizar al abrir y avisar al actualizar.|  
|Proveedores de datos confiables|MSOLAP.4<br /><br /> MSOLAP.5|MSOLAP.4 está incluido de forma predeterminada, pero el acceso a datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] requiere que el proveedor de MSOLAP.4 sea la versión SQL Server 2008 R2.<br /><br /> MSOLAP.5 se instala con la versión [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint.<br /><br /> No quite estos proveedores de la lista de proveedores de datos confiables. En algunos casos, es posible que tenga que instalar copias adicionales de este proveedor en otros servidores de SharePoint de la granja. Para obtener más información, consulte [Instalar el proveedor OLE DB de Analysis Services en servidores de SharePoint](http://msdn.microsoft.com/en-us/2c62daf9-1f2d-4508-a497-af62360ee859).|  
|Bibliotecas de conexiones de datos confiables|Opcional.|Puede usar archivos de conexión de datos de Office (.odc) en libros [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Si utiliza archivos .odc para proporcionar información de conexión a libros [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] locales, puede agregar los mismos archivos .odc a esta biblioteca.|  
|Ensamblados de funciones definidas por el usuario|No aplicable.|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint omite los ensamblados de funciones definidas por el usuario que implemente para Excel Services. Si confía en los ensamblados definidos por el usuario para conseguir un comportamiento determinado, tenga en cuenta que el procesamiento de consultas de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no usará las funciones definidas por el usuario que ha creado.|  
  
## <a name="see-also"></a>Vea también  
 [Configurar las cuentas de servicio Power Pivot](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts.md)   
 [Configuración de Power Pivot (Power Pivot para SharePoint) de la cuenta de actualización de datos desatendida](http://msdn.microsoft.com/en-us/81401eac-c619-4fad-ad3e-599e7a6f8493)   
 [Crear una ubicación de confianza para los sitios PowerPivot en Administración central](../../analysis-services/power-pivot-sharepoint/create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)   
 [Arquitectura de seguridad de Power Pivot](http://go.microsoft.com/fwlink/?linkID=220970)  
  
  
