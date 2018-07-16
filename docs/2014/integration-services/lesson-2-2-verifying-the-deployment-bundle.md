---
title: 'Paso 2: Comprobar el conjunto de implementación | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6c13f5c9-c75e-4e52-94dc-2d2db2c578fe
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f43403ee078b66226839ecc934cf83a99751f76a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37273431"
---
# <a name="step-2-verifying-the-deployment-bundle"></a>Paso 2: Comprobar el paquete de implementación
  En la lección 1, ha creado el proyecto Deployment Tutorial y le ha agregado paquetes y archivos auxiliares; en la tarea anterior, ha creado una utilidad de implementación para el proyecto.  
  
 En esta tarea, comprobará el contenido del paquete de implementación. El paquete de implementación es la carpeta que copiará en el equipo de destino y que usará para instalar paquetes. Si ha usado el valor predeterminado, bin\Deployment, como ubicación de la utilidad de implementación, el paquete de implementación está en la carpeta Bin\Deployment dentro de la carpeta Deployment Tutorial del proyecto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
### <a name="to-verify-the-content-of-deployment-bundle"></a>Para comprobar el contenido del paquete de implementación  
  
1.  Busque la carpeta bin\Deployment en el equipo.  
  
2.  Compruebe que están presentes los archivos siguientes:  
  
    -   DataTransfer.dtsx  
  
    -   datatransferconfig.dtsconfig  
  
    -   Deployment Tutorial.SSISDeploymentManifest  
  
    -   LoadXMLData.dtsx  
  
    -   loadxmldataconfig.dtsconfig  
  
    -   NewCustomers.txt  
  
    -   orders.xml  
  
    -   orders.xsd  
  
    -   Readme.txt  
  
3.  Haga clic con el botón derecho en Deployment Tutorial.SSISDeploymentManifest, elija **Abrir con**y, después, haga clic en **Internet Explorer**. También puede abrir el archivo en un editor de texto como el Bloc de notas. El código XML del archivo debe ser el siguiente:  
  
     `<?xml version="1.0"?><DTSDeploymentManifest GeneratedBy="Domain\UserName" GeneratedFromProjectName="Deployment Tutorial" GeneratedDate="2006-02-24T13:29:02.6537669-08:00" AllowConfigurationChanges="true"><Package>DataTransfer.dtsx</Package><Package>LoadXMLData.dtsx</Package><ConfigurationFile>datatransferconfig.dtsconfig</ConfigurationFile><ConfigurationFile>loadxmldataconfig.dtsconfig</ConfigurationFile><MiscellaneousFile>Readme.txt</MiscellaneousFile><MiscellaneousFile>orders.xml</MiscellaneousFile><MiscellaneousFile>NewCustomers.txt</MiscellaneousFile><MiscellaneousFile>orders.xsd</MiscellaneousFile></DTSDeploymentManifest>`  
  
4.  Compruebe que el valor de la `AllowConfigurationChanges` atributo es **true** y el XML incluye un `Package` (elemento) para cada uno de los dos paquetes, un `MiscellaneousFile` (elemento) para cada uno de los cuatro archivos no empaquetados y un `ConfigurationFile` elemento para cada uno de los dos archivos de configuración XML.  
  
5.  Salga de Internet Explorer o del editor de texto.  
  
## <a name="next-lesson"></a>Lección siguiente  
 [Lección 3: Instalar paquetes](../integration-services/lesson-3-install-ssis-package.md)  
  
![Icono de Integration Services (pequeño)](media/dts-16.gif "icono de Integration Services (pequeño)")**mantenerse actualizado con Integration Services  **<br /> Para obtener las descargas, artículos, ejemplos y vídeos más recientes de Microsoft, así como soluciones seleccionadas de la comunidad, visite la página de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en MSDN:<br /><br /> [Visite la página de Integration Services en MSDN](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para recibir notificaciones automáticas de estas actualizaciones, suscríbase a las fuentes RSS disponibles en la página.  
  
  
