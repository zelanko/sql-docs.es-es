---
title: Seleccione el origen de datos | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.rtp.rptwizard.selectdatasource.f1
ms.assetid: cdd84ad8-7c6a-41ac-bf51-1b0973434829
caps.latest.revision: 31
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 8cb8cb384b83c4d5ca8ba16e017cbf79d53f3742
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36202649"
---
# <a name="select-the-data-source"></a>Seleccionar el origen de datos
  Utilice esta página del Asistente para informes para definir un origen de datos para el informe.  
  
## <a name="options"></a>Opciones  
 **Origen de datos compartido**  
 Seleccione **Origen de datos compartido** para usar un origen de datos compartido predefinido que tiene ya la información de conexión del origen de datos que quiere usar. La lista contiene todos los orígenes de datos compartidos que se incluyen en el proyecto.  
  
 **Nuevo origen de datos**  
 Seleccione **Nuevo origen de datos** para definir un nuevo origen de datos. La información del origen de datos se utilizará solamente con el informe actual.  
  
 **Nombre**  
 Escriba un nombre para la conexión con el origen de datos. Dicho nombre debe ser único en el informe.  
  
 **Tipo**  
 Seleccione el tipo de origen de datos que está usando (por ejemplo, si está usando una base de datos [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], elija [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]).  
  
 **Cadena de conexión**  
 Escriba una cadena de conexión para el origen de datos. Para obtener más información acerca de las cadenas de conexión, vea [las conexiones de datos, orígenes de datos y cadenas de conexión en Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md).  
  
 Haga clic en **Editar** para especificar el servidor del origen de datos en el cuadro de diálogo **Propiedades de conexión** . Puede especificar un origen de datos local o remoto.  
  
 Haga clic en **Credenciales** para suministrar las credenciales de la base de datos. Como mínimo, las credenciales que especifique deben ser suficientes para poder conectarse al origen de datos con fines de diseño de informes. Cuando el informe se implemente en un servidor de informes, las credenciales de la base de datos deben adaptarse a todos los usuarios del informe. Por ejemplo, si quiere que todos los usuarios del informe se conecten al origen de datos usando sus credenciales, elija **Usar autenticación de Windows (seguridad integrada)**. Las credenciales que especifique deben ser válidas para el origen de datos; por tanto, si elige la autenticación de Windows, asegúrese de que el origen de datos acepta las conexiones de todas las cuentas de usuario que ejecutarán el informe. Las credenciales de la base de datos pueden administrarse independientemente del informe. Para obtener más información, vea [Administrar orígenes de datos de informe](report-data/manage-report-data-sources.md).  
  
 **Convertir en origen de datos compartido**  
 Seleccione esta opción para almacenar el origen de datos en el proyecto como origen de datos compartido, en lugar de en el informe. De ese modo, puede utilizarlo como origen de datos para otros informes en el proyecto.  
  
## <a name="see-also"></a>Vea también  
 [Incrustados y compartidos conexiones de datos u orígenes de datos &#40;el generador de informes SSRS&#41;](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md)   
 [Especificar información de credenciales y conexión para los orígenes de datos de informes](report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [Servidor de informes de Reporting Services](../../2014/reporting-services/reporting-services-report-server.md)   
 [Archivo de configuración RSReportDesigner](report-server/rsreportdesigner-configuration-file.md)   
 [Las conexiones de datos, orígenes de datos y cadenas de conexión en Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [Ayuda del Asistente para informes](../../2014/reporting-services/report-wizard-help.md)  
  
  