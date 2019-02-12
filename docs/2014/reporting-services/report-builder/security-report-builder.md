---
title: Seguridad (Generador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: ed38291a-6afe-449f-9f32-3ae04502bd6f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5f5d8f6f88f862486a50b0e7365bb221acb0138e
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56015026"
---
# <a name="security-report-builder"></a>Seguridad (Generador de informes)
  El Generador de informes es una aplicación cliente de creación de informes diseñada para que funcione con un servidor de informes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . El servidor de informes se puede configurar para funcione en modo nativo como un servidor independiente o en modo integrado de SharePoint, para que admita los informes de un sitio de SharePoint.  
  
 En el Generador de informes puede crear informes, conjuntos de datos compartidos y elementos de informe reutilizables. Desde un servidor de informes o sitio de SharePoint, puede editar los informes y agregar orígenes de datos compartidos, conjuntos de datos compartidos y elementos de informe compartidos.  
  
 Para crear, publicar y usar informes y elementos relacionados con los informes, debe comprender la relación entre las características de seguridad y los siguientes aspectos:  
  
-   **Servidor de informes o sitio de SharePoint donde publica los informes.** El administrador del servidor de informes o del sitio de SharePoint administra estas características.  
  
-   **Informes publicados y elementos relacionados con los informes** Son elementos relacionados con los informes los orígenes de datos compartidos y sus credenciales, conjuntos de datos compartidos, parámetros, elementos de informe y modelos de informe. El autor del informe administra las características de seguridad correspondientes a estos elementos. El autor del informe debe obtener del administrador del servidor de informes o del sitio de SharePoint los permisos necesarios para publicar y compartir los elementos.  
  
-   **Orígenes de datos externos utilizados en un informe.** El propietario del origen de datos externo administra estas características.  
  
-   **Modelos de informe basados en orígenes de datos externos** El diseñador de modelos administra estas características.  
  
-   **Características de informe interactivas como los parámetros.** El autor del informe administra estas características.  
  
 Revise la información de este tema para saber cómo utilizar las características de seguridad para administrar y proteger mejor los informes y los elementos relacionados con los informes.  
  
##  <a name="ReportServers"></a> Descripción de la seguridad de los servidores de informes  
 La publicación y visualización de informes son operaciones que requieren permisos. El administrador de un servidor de informes concede permisos para asegurarse de que solo los usuarios autorizados pueden publicar y ver los informes de uno de los siguientes tipos de servidores de informes:  
  
-   Servidor de informes configurado en modo nativo  
  
     Para conectarse a un servidor de informes o desplazarse hasta él, debe tener una dirección URL válida y los permisos necesarios para obtener acceso al servidor.  
  
     Para ver o publicar elementos en un servidor de informes, los conjuntos de permisos que se aplican a los elementos y las operaciones relacionados con los informes se organizan en roles. El administrador de un servidor de informes asigna a cada usuario a uno o varios roles. Por ejemplo, el rol predefinido Explorador permite ver informes, carpetas, modelos y recursos.  
  
     Si no puede conectarse o desplazarse a un servidor de informes, póngase en contacto con el administrador del servidor de informes. Para más información, vea [Seguridad y protección de Reporting Services](../security/reporting-services-security-and-protection.md) en la documentación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] de los [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [Books Online](https://go.microsoft.com/fwlink/?linkid=121312).  
  
-   Servidor de informes configurado en el modo integrado de SharePoint  
  
     Para conectarse a un sitio de SharePoint integrado con un servidor de informes, debe tener una dirección URL válida para sitio o subsitio de SharePoint y los permisos de acceso necesarios.  
  
     Los permisos para obtener acceso a los elementos y a las operaciones relacionados con los informes se conceden a través de directivas de seguridad de SharePoint que asignan una cuenta de usuario o grupo a un nivel de permiso relativo a un elemento.  
  
     Si no puede conectarse a un sitio o subsitio de SharePoint, o no puede examinarlo, póngase en contacto con el administrador del sitio de SharePoint.  
  
=
  
##  <a name="Reports"></a> Descripción de la seguridad de los informes publicados y los elementos relacionados con los informes  
 El administrador del servidor de informes administra la seguridad de los informes y los elementos relacionados con los informes. Son elementos relacionados con los informes los orígenes de datos incrustados y compartidos como credenciales, conjuntos de datos compartidos, parámetros, elementos de informe y modelos.  
  
 En un servidor de informes o sitio de SharePoint, los informes y elementos y operaciones relacionados con los informes se pueden proteger por separado. Los permisos para obtener acceso a los elementos y a las operaciones se conceden a través de directivas de seguridad que asignan una cuenta de usuario o grupo a un nivel de permiso relativo a un elemento. Para reducir la complejidad y la sobrecarga de mantener un gran número de directivas, los elementos de un contenedor, como una carpeta, heredan los permisos del contenedor. Por ejemplo, si un usuario tiene el permiso concreto Ver informes en una carpeta, tiene dicho permiso para los elementos de la carpeta.  
  
 Los permisos se pueden invalidar en elementos o carpetas mediante la seguridad del nivel de elemento. Cuando se aplica la seguridad del nivel de elemento, el elemento deja de heredar los permisos del contenedor primario. Si se aplica la seguridad del nivel de elemento a una carpeta, las carpetas anidadas heredan los mismos permisos.  
  
 Si no puede desplazarse a elementos que otro usuario ha publicado para usted, ni puede buscarlos, es posible que haya un problema con los permisos para el elemento o la carpeta.  
  
 Para que otros usuarios puedan desplazarse a elementos que ha publicado para compartirlos, y puedan buscarlos, debe trabajar con el administrador del servidor de informes para establecer una organización de carpetas que proporcione acceso a los usuarios. Los permisos deben proporcionar acceso de creación de informes y de ejecución de informes publicados.  
  
 Para obtener más información, consulte los siguientes temas en la documentación relativa a [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en los [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [de](https://go.microsoft.com/fwlink/?linkid=121312):  
  
-   [Roles y permisos &#40;Reporting Services&#41;](../security/roles-and-permissions-reporting-services.md)  
  
-   [Administración de conjuntos de datos compartidos](../report-data/manage-shared-datasets.md)  
  
### <a name="update-notifications-for-report-parts"></a>Actualizar notificaciones de los elementos de informe  
 Los elementos de informe se publican en un servidor de informes para que otros usuarios puedan compartirlos. Por cuestiones de diseño, se especifica la ubicación en la que se deben publicar los elementos de informe.  
  
 Los usuarios que incluyen elementos de informe en los informes pueden habilitar la característica de actualización. Cuando esta característica está habilitada, los usuarios reciben notificaciones cuando los elementos de informe cambian en el servidor de informes.  
  
 Si se cambia la ubicación original de los elementos de informe, el aviso de actualización indica las ubicaciones actual y anterior del elemento de informe. Acepte solo las actualizaciones de ubicaciones de confianza.  
  
 Para más información, vea [Elementos de informe &#40;Generador de informes y SSRS&#41;](../report-parts-report-builder-and-ssrs.md).  
  
=  
  
##  <a name="Data"></a> Descripción de la seguridad de los datos de informe y los orígenes de datos externos  
 Para tener acceso a los datos de cada origen de datos externo de un informe, debe crear origen de datos incrustado o agregar una referencia a un origen de datos compartido o conjunto de datos compartido en el informe.  
  
 Para cada origen de datos externo, debe proporcionar credenciales suficientes para tener acceso al origen y los datos subyacentes. El propietario del origen de datos especifica el tipo de credenciales que proporciona este acceso.  
  
 Las credenciales no se guardan en la definición de informe. Se administran independientemente del informe en el servidor de informes o sitio de SharePoint y en el cliente de creación de informes.  
  
 En el momento del diseño de informe, las credenciales se utilizan para ejecutar consultas de conjunto de datos y obtener la vista previa del informe. En tiempo de ejecución, las credenciales se utilizan para ejecutar el informe y almacenar en caché los resultados de la consulta. También puede almacenar en memoria caché por separado los resultados de la consulta del conjunto de datos compartido. Las credenciales del tiempo de diseño y las del tiempo de ejecución pueden ser distintas. Para más información, vea [Especificar credenciales en el Generador de informes](../specify-credentials-in-report-builder.md).  
  
 Para obtener más información acerca de cómo proteger los datos, consulte el siguiente tema en la documentación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [Libros en pantalla](https://go.microsoft.com/fwlink/?linkid=121312):  
  
-   [Centro de seguridad para el motor de base de datos SQL Server y la base de datos SQL Azure](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
 Para más información sobre orígenes de datos, vea [Conexiones de datos, orígenes de datos y cadenas de conexión en el Generador de informes](../data-connections-data-sources-and-connection-strings-in-report-builder.md).  
  
=
  
##  <a name="Models"></a> Descripción de los modelos y los filtros de seguridad  
 Cuando se recuperan datos de un modelo de informe basado en datos externos, puede aplicar filtros de seguridad en el modelo. De esta manera se protegen los datos de forma que cada usuario que ejecuta un informe pueda ver solo los datos para los que tiene permiso.  
  
 Los parámetros de informe no se utilizan para la seguridad en el nivel de fila; no evitan que los usuarios o grupos de usuarios vean filas de datos específicas. Para aplicar seguridad a los datos que se muestran en un informe, es necesario utilizar filtros de seguridad o seguridad de elemento de modelo.  
  
=
  
##  <a name="Interactive"></a> Descripción de la seguridad de las características interactivas en la creación de informes  
 A menudo, los informes utilizan parámetros para que un usuario pueda personalizar interactivamente la vista de un informe. A continuación se ofrecen algunas sugerencias para diseñar informes correctamente:  
  
-   No utilice parámetros basados en parámetros de consulta y que son de tipo **Texto** , a menos que proporcione valores válidos. Una lista de valores disponibles ayuda al usuario a elegir solo valores válidos. Sin una lista de valores disponibles, no se pueden restringir los valores que puede especificar un usuario.  
  
-   No utilice el global [& UserID] para proteger datos privados. Como parámetro de informe, este valor se puede especificar en una dirección URL de informe mediante sintaxis de acceso a dirección URL. El uso de este valor en una expresión en un conjunto de datos compartido evita que el conjunto de datos se almacene en memoria caché. Para más información, vea [Referencia de parámetros de acceso URL](../url-access-parameter-reference.md) en la documentación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] de los [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [Books Online](https://go.microsoft.com/fwlink/?linkid=121312).  
  
 Después de la publicación de elementos en un servidor de informes, el administrador del servidor de informes puede contribuir a protegerlos asignando seguridad del nivel de rol o seguridad del nivel de carpeta y elemento. Para más información, vea [Proteger informes y recursos](../security/secure-reports-and-resources.md) en la documentación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en los [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [Books Online](https://go.microsoft.com/fwlink/?linkid=121312).  
  
 
  
## <a name="see-also"></a>Vea también  
 [Instalar, desinstalar y asistencia del generador de informes](../install-uninstall-and-report-builder-support.md)   
 [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)  
  
  
