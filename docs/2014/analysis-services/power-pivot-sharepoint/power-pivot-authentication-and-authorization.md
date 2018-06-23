---
title: PowerPivot Authentication and Authorization | Documentos de Microsoft
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 48230cc0-4037-4f99-8360-dadf4bc169bd
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: e24a764afb7aae49194847354800e580da88a9a1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36197265"
---
# <a name="powerpivot-authentication-and-authorization"></a>Autenticación y autorización de PowerPivot
  Una implementación de PowerPivot para SharePoint que se ejecuta dentro de una granja de servidores de SharePoint 2010 usa el subsistema de autenticación y el modelo de autorización que proporcionan los servidores de SharePoint. La infraestructura de seguridad de SharePoint se extiende al contenido y a las operaciones de PowerPivot porque todo el contenido relacionado con PowerPivot está almacenado en bases de datos de contenido de SharePoint, y todas las operaciones relacionadas con PowerPivot las realizan los servicios compartidos de PowerPivot en la granja. Los usuarios que solicitan un libro que contiene los datos PowerPivot se autentican usando una identidad de usuario de SharePoint que se basa en su identidad de usuario de Windows. Los permisos para ver el libro determinan si la solicitud se concede o se deniega.  
  
 Dado que para el análisis de los datos de autoservicio se requiere la integración con Excel Services, la protección de un servidor de PowerPivot requiere que también se conozca la seguridad de Excel Services. Cuando un usuario consulta una tabla dinámica que tiene una conexión de datos a datos PowerPivot, Excel Services reenvía una solicitud de conexión de datos a un servidor de PowerPivot de la granja para cargar los datos. Esta interacción entre los servidores requiere saber cómo establecer una configuración de seguridad para ambos.  
  
 Haga clic en los siguientes vínculos para leer secciones concretas de este tema:  
  
 [Autenticación de Windows con el requisito de inicio de sesión de modo clásico](power-pivot-authentication-and-authorization.md#bkmk_auth)  
  
 [Operaciones de PowerPivot que requieren la autorización del usuario](#UserConnections)  
  
 [Permisos de SharePoint para el acceso a datos PowerPivot](#Permissions)  
  
 [Consideraciones de seguridad de Excel Services para los libros PowerPivot](#excel)  
  
##  <a name="bkmk_auth"></a> Autenticación de Windows mediante el inicio de sesión en modo clásico  
 PowerPivot para SharePoint admite un conjunto reducido de las opciones de autenticación disponibles en SharePoint. De las opciones de autenticación disponibles, solo se admite la autenticación de Windows para una implementación de PowerPivot para SharePoint. Además, la aplicación web a través de la que se produce el inicio de sesión debe estar configurada para el modo clásico.  
  
 Se requiere la autenticación de Windows porque el motor de datos de Analysis Services de una implementación de PowerPivot para SharePoint solo admite este tipo de autenticación. Excel Services establece conexiones con Analysis Services a través del proveedor OLE DB MSOLAP mediante una identidad de usuario de Windows que se ha autenticado a través de NTLM o del protocolo Kerberos.  
  
 El segundo requisito, la autenticación en modo clásico en la aplicación web, es necesario para asegurarse de que el servicio web PowerPivot funciona. El servicio web es un componente que se ejecuta en un servidor web front-end y que proporciona redirección HTTP a un servidor PowerPivot para SharePoint de la granja. Mientras que el servicio web dispone de notificaciones para las comunicaciones entre servicios, no dispone de ellas para las solicitudes de conexión de datos que enruta a un servicio compartido PowerPivot de la granja. Las solicitudes para cargar los datos PowerPivot solo se admiten en las conexiones autenticadas que proceden de IIS y usan una identidad de Windows. El inicio de sesión en modo clásico en la aplicación web es lo que permite una conexión correcta desde el servicio web PowerPivot a los servicios compartidos de PowerPivot en la granja.  
  
 Aunque el inicio de sesión en modo clásico no es necesario en el escenario de acceso a datos más frecuente (cuando los datos PowerPivot se extraen del mismo libro de Excel que los representa), no intente usar PowerPivot para SharePoint con aplicaciones web de SharePoint configuradas para usar otros proveedores de autenticación. Si lo hace, se producirá un error de conexión cada vez que los usuarios intenten conectar con libros PowerPivot como origen de datos externo.  
  
 Sin el inicio de sesión en modo clásico, fallarán los siguientes tipos de solicitudes administradas por el servicio web de PowerPivot:  
  
-   Cualquier solicitud de datos de PowerPivot que se origine desde fuera de la granja (por ejemplo, creando un informe en el Diseñador de informes o en el Generador de informes, donde el origen de datos es una URL de SharePoint que apunta a un libro PowerPivot)  
  
-   Las solicitudes originadas en la granja desde una aplicación cliente o informes que usen un libro PowerPivot como origen de datos externo (crear un libro en la aplicación de escritorio de Excel, usando como origen de datos un segundo libro de Excel publicado que contiene datos PowerPivot)  
  
### <a name="how-to-check-the-authentication-provider-for-your-application"></a>Comprobar el proveedor de autenticación para la aplicación  
 Cuando cree nuevas aplicaciones web, asegúrese de seleccionar la opción **Modo clásico de autenticación** en la página Crear nueva aplicación web.  
  
 En el caso de aplicaciones web existentes, use las siguientes instrucciones para comprobar que la aplicación web está configurada para usar la autenticación de Windows.  
  
1.  En Administración central, en Administración de aplicaciones, haga clic en **Administrar las aplicaciones web**.  
  
2.  Seleccione la aplicación web.  
  
3.  Haga clic en **Proveedores de autenticación**.  
  
4.  Compruebe que tiene un proveedor para cada zona, y que la zona predeterminada está establecida en Windows.  
  
##  <a name="UserConnections"></a> Operaciones de PowerPivot que requieren la autorización del usuario  
 La autorización de SharePoint se usa exclusivamente para todos los niveles de acceso al procesamiento de datos y las consultas de PowerPivot.  
  
 No se admite el modelo de autorización basada en roles de Analysis Services. No hay ninguna autorización basada en roles para los datos PowerPivot en el nivel de celda, fila o tabla. No puede proteger partes diferentes del libro para conceder o denegar el acceso a la información confidencial que contiene para usuarios concretos. Los datos PowerPivot incrustados están completamente disponibles para los usuarios que tienen permisos para ver el libro de Excel en una biblioteca de SharePoint.  
  
 PowerPivot para SharePoint suplantará a un usuario de SharePoint en los casos siguientes:  
  
-   Consultas a tablas dinámicas o gráficos dinámicos que tengan conexiones de datos a una base de datos PowerPivot, donde una aplicación de servicio PowerPivot establece las conexiones en nombre de un usuario a una instancia de servicio compartido PowerPivot concreta que procesa los datos.  
  
-   La carga de datos PowerPivot de la memoria caché o de una biblioteca, si los datos no están disponibles de otra forma. Si se realiza una solicitud de conexión de datos para datos PowerPivot que aún no está cargados en el sistema, la instancia de [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] usará la identidad del usuario de SharePoint para recuperar el origen de datos de una biblioteca de contenido y cargarlo en la memoria.  
  
-   Las operaciones de actualización de datos que guardan una copia actualizada del origen de datos al libro en una biblioteca de contenido. En este caso, se realiza un registro real de la operación utilizando el nombre de usuario y la contraseña que se recuperan de una aplicación de destino en el Servicio de almacenamiento seguro. Las credenciales pueden ser la cuenta de actualización de datos desatendida de PowerPivot o las credenciales que se almacenaron con la programación de actualización de datos al crearse. Para obtener más información, consulte [configurar las credenciales almacenadas para la actualización de datos de PowerPivot &#40;PowerPivot para SharePoint&#41; ](../configure-stored-credentials-data-refresh-powerpivot-sharepoint.md) y [configurar la cuenta de actualización de datos desatendida de PowerPivot &#40; PowerPivot para SharePoint&#41;](../configure-unattended-data-refresh-account-powerpivot-sharepoint.md).  
  
##  <a name="Permissions"></a> Permisos de SharePoint para el acceso a datos PowerPivot  
 La publicación, administración y protección de un libro PowerPivot solamente se admite a través de la integración de SharePoint. Los servidores de SharePoint proporcionan subsistemas de autenticación y autorización que se aseguran de que se produce un acceso legítimo a los datos. No hay ningún escenario admitido para implementar de forma segura un libro PowerPivot fuera de una granja de servidores de SharePoint.  
  
 El acceso de usuario a los datos PowerPivot del servidor es de solo lectura mediante permisos para ver o superiores. Los permisos de contribución permiten agregar y modificar el archivo. Las modificaciones en los datos PowerPivot requieren la descarga del libro a una aplicación de escritorio de Excel que tenga instalado PowerPivot para Excel. Los permisos de contribución en el archivo determinarán si el usuario puede descargar el archivo localmente y guardar los cambios de nuevo en SharePoint.  
  
 Por tanto, los niveles de permisos Contribuir y Solo ver definen el conjunto vigente de permisos para el acceso de los usuarios a los datos PowerPivot. Otros niveles de permisos funcionan hasta el punto en que tienen los mismos permisos que Contribuir y Solo ver (por ejemplo, dado que Lectura incluye los permisos Solo ver, un usuario al que se le asigne Lectura tendrá el mismo acceso que otro con el permiso Solo ver).  
  
 En la siguiente tabla se resumen los niveles de permisos que determinan el acceso a los datos PowerPivot y operaciones del servidor:  
  
|Nivel del permiso|Permite estas tareas|  
|----------------------|------------------------|  
|Administrador de granja o de servicio|Instalar, habilitar y configurar servicios y aplicaciones.<br /><br /> Usar el panel de administración de PowerPivot y ver informes administrativos.|  
|Control total|Activar la integración de características de PowerPivot en el nivel de colección de sitios.<br /><br /> Crear una biblioteca de la galería de PowerPivot.<br /><br /> Crear una biblioteca de fuentes de distribución de datos.|  
|Contribución|Agregar, modificar, eliminar y descargar libros PowerPivot.<br /><br /> Configurar actualización de datos.<br /><br /> Crear nuevos libros e informes basados en libros PowerPivot en un sitio de SharePoint.<br /><br /> Crear documentos de servicio de datos en una biblioteca de fuentes de distribución de datos.|  
|Lectura|Acceder a libros PowerPivot como origen de datos externo, donde la URL del libro se escribe explícitamente en un cuadro de diálogo de conexión (por ejemplo, en el Asistente para conexión de datos de Excel).|  
|Solo ver|Ver libros PowerPivot.<br /><br /> Ver el historial de la actualización de datos.<br /><br /> Conectarse con un libro local a un libro PowerPivot en un sitio de SharePoint, para cambiar sus datos de otras maneras.<br /><br /> Descargue una instantánea del libro. La instantánea es una copia estática de los datos, segmentaciones de datos, filtros, fórmulas ni conexiones de datos. El contenido de la instantánea es parecido al que se obtiene al copiar los valores de las celdas de la ventana del explorador.|  
  
##  <a name="excel"></a> Consideraciones de seguridad de Excel Services para los libros PowerPivot  
 El procesamiento de consultas de PowerPivot en el lado servidor está unido estrechamente a los servicios de Excel. La integración de productos comienza en el nivel de documento, donde los libros PowerPivot son archivos de libro de Excel (.xlsx) que contienen o hacen referencia a datos PowerPivot. No hay ninguna extensión de archivo independiente para un libro PowerPivot.  
  
 Cuando un libro PowerPivot se abre en un sitio de SharePoint, Excel Services lee las cadenas de conexión de datos PowerPivot incrustadas y reenvía la solicitud al proveedor OLE DB de Analysis Services de SQL Server local. A continuación, el proveedor pasa la información de conexión a un servidor de PowerPivot en la granja. Para que la solicitud fluya uniformemente entre los dos servidores, Excel Services se debe configurar para usar valores que son requeridos por PowerPivot para SharePoint.  
  
 En Excel Services, la configuración relativa a la seguridad se especifica en las ubicaciones confiables, proveedores de datos confiables y bibliotecas de conexiones de datos confiables. En la siguiente tabla se describen los valores que habilitan o mejoran el acceso a datos PowerPivot. Si no aparece aquí un valor, no tiene ningún efecto en las conexiones con el servidor de PowerPivot. Para obtener instrucciones sobre cómo especificar estos valores paso a paso, vea la sección "Habilitar Excel Services" en [configuración inicial &#40;PowerPivot para SharePoint&#41;](../../sql-server/install/initial-configuration-powerpivot-for-sharepoint.md).  
  
> [!NOTE]  
>  La mayoría de la configuración relacionada con la seguridad se aplica a las ubicaciones confiables. Si desea conservar los valores predeterminados o usar valores diferentes para sitios distintos, puede crear una ubicación confiable adicional para sitios que contienen datos PowerPivot y, a continuación, configurar los siguientes valores solo para ese sitio. Para obtener más información, consulte [Create a trusted location for PowerPivot sites in Central Administration](create-a-trusted-location-for-power-pivot-sites-in-central-administration.md).  
  
|Área|Configuración|Descripción|  
|----------|-------------|-----------------|  
|Aplicación web|Proveedor de autenticación de Windows|PowerPivot convierte un token de notificación que obtiene de Excel Services en una identidad de usuario de Windows. Cualquier aplicación web que use Excel Services como un recurso se debe configurar para usar el proveedor de autenticación de Windows.|  
|Ubicación confiable|Tipo de ubicación|Este valor debe estar establecido en **Microsoft SharePoint Foundation**. Los servidores de PowerPivot recuperan una copia del archivo .xlsx y la cargan en un servidor de Analysis Services en la granja. El servidor solo puede recuperar archivos .xlsx de una biblioteca de contenidos.|  
||Permitir datos externos|Este valor debe estar establecido en **Bibliotecas de conexiones de datos de confianza e incrustadas**. Los libros PowerPivot contienen conexiones de datos incrustadas. Si deniega las conexiones incrustadas, los usuarios pueden ver la memoria caché de la tabla dinámica, pero no podrán utilizar los datos PowerPivot.|  
||Avisar al actualizar|Este valor debería estar deshabilitado si está usando la galería de PowerPivot para almacenar libros e informes. La galería de PowerPivot incluye una característica de vista previa de documentos que funciona mejor si están desactivadas actualizar al abrir y Avisar al actualizar.|  
|Proveedores de datos confiables|MSOLAP.4<br /><br /> MSOLAP.5|MSOLAP.4 está incluido de forma predeterminada, pero el acceso a datos PowerPivot requiere que el proveedor de MSOLAP.4 sea la versión SQL Server 2008 R2.<br /><br /> MSOLAP.5 se instala con la versión [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] de PowerPivot para SharePoint.<br /><br /> No quite estos proveedores de la lista de proveedores de datos confiables. En algunos casos, es posible que tenga que instalar copias adicionales de este proveedor en otros servidores de SharePoint de la granja. Para obtener más información, consulte [Instalar el proveedor OLE DB de Analysis Services en servidores de SharePoint](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md).|  
|Bibliotecas de conexiones de datos confiables|Opcional.|Puede usar archivos de conexión de datos de Office (.odc) en libros PowerPivot. Si utiliza archivos .odc para proporcionar información de conexión a libros PowerPivot locales, puede agregar los mismos archivos .odc a esta biblioteca.|  
|Ensamblados de funciones definidas por el usuario|No aplicable.|PowerPivot para SharePoint omite los ensamblados de funciones definidas por el usuario que implemente para Excel Services. Si confía en los ensamblados definidos por el usuario para conseguir un comportamiento determinado, tenga en cuenta que el procesamiento de consultas de PowerPivot no usará las funciones definidas por el usuario que ha creado.|  
  
## <a name="see-also"></a>Vea también  
 [Configurar cuentas de servicio PowerPivot](configure-power-pivot-service-accounts.md)   
 [Configurar PowerPivot cuenta de actualización de datos desatendida &#40;PowerPivot para SharePoint&#41;](../configure-unattended-data-refresh-account-powerpivot-sharepoint.md)   
 [Crear una ubicación de confianza para sitios PowerPivot en Administración Central](create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)   
 [Arquitectura de seguridad de PowerPivot](http://go.microsoft.com/fwlink/?linkID=220970)  
  
  