---
title: Cuadro de diálogo de propiedades de origen de datos compartido, las credenciales | Documentos de Microsoft
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.rtp.rptdesigner.shareddatasource.credentials.f1
ms.assetid: c08d1a5f-206b-4d53-ab1a-368b651ee5bb
caps.latest.revision: 28
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 4956317c08b1f48e6504122e30392426e3dbcfcd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36112605"
---
# <a name="shared-data-source-properties-dialog-box-credentials"></a>Propiedades del origen de datos compartidos (cuadro de diálogo), Credenciales
  Seleccione **Credenciales** en el cuadro de diálogo **Propiedades del origen de datos compartidos** para mostrar y modificar las credenciales para conectarse a un origen de datos compartido en el informe. Las credenciales que proporcione se usarán para tener acceso al origen de datos y almacenar en caché una copia de los datos para la vista previa de los informes. Para obtener más información sobre cómo almacenar en caché datos de la vista previa, vea [Obtener la vista previa de informes](reports/previewing-reports.md). Para obtener más información sobre las credenciales, vea [Especificar información de credenciales y conexión para los orígenes de datos de informes](report-data/specify-credential-and-connection-information-for-report-data-sources.md).  
  
## <a name="options"></a>Opciones  
 **Utilizar autenticación de Windows (seguridad integrada)**  
 Seleccione esta opción para utilizar la autenticación de Windows.  
  
 **Use este nombre de usuario y contraseña**  
 Seleccione esta opción para proporcionar un nombre de usuario y una contraseña específicos. Para los orígenes de datos compartidos: al publicar el proyecto de servidor de informes en el servidor de destino, el nombre de usuario y la contraseña se guardan como las credenciales almacenadas para la base de datos. Si desea usar el nombre de usuario y la contraseña como credenciales de Windows, puede editar las propiedades del origen de datos compartido publicado en el servidor de destino. Para más información, vea [Crear, eliminar o modificar un origen de datos compartido &#40;Administrador de informes&#41;](../../2014/reporting-services/create-delete-or-modify-a-shared-data-source-report-manager.md).  
  
 **Nombre de usuario.**  
 Escriba un nombre de usuario con el que iniciar sesión en el origen de datos.  
  
 **Contraseña**  
 Escriba una contraseña con la que iniciar sesión en el origen de datos.  
  
 **Pedir credenciales**  
 Seleccione esta opción para solicitar las credenciales al ejecutar el informe.  
  
 **Escriba la cadena de mensaje**  
 Escriba una frase para pedir al usuario que proporcione las credenciales de inicio de sesión para el origen de datos.  
  
 **Sin credenciales**  
 Seleccione esta opción si no desea proporcionar credenciales para el origen de datos. Esta opción solo funciona si el origen de datos no acepta credenciales o si se pasan credenciales de otra manera.  
  
## <a name="see-also"></a>Vea también  
 [Las conexiones de datos, orígenes de datos y cadenas de conexión en Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [Especificar información de credenciales y conexión para los orígenes de datos de informes](report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [Cuadro de diálogo de propiedades de origen de datos compartidos, General](../../2014/reporting-services/shared-data-source-properties-dialog-box-general.md)  
  
  