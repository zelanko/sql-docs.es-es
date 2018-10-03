---
title: 'Paso 2: Comprobar el conjunto de implementación | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 6c13f5c9-c75e-4e52-94dc-2d2db2c578fe
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 74d17c1ceb03cfc452a925d41fdeab98c6f90339
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47654418"
---
# <a name="lesson-2-2---verifying-the-deployment-bundle"></a>Lección 2-2: Comprobar el conjunto de implementación
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
  
4.  Compruebe que el valor del atributo **AllowConfigurationChanges** es **true** y el XML incluye un elemento **Package** para cada uno de los dos paquetes, un elemento **MiscellaneousFile** para cada uno de los cuatro archivos no empaquetados y un elemento **ConfigurationFile** para cada uno de los dos archivos de configuración de XML.  
  
5.  Salga de Internet Explorer o del editor de texto.  
  
## <a name="next-lesson"></a>Lección siguiente  
[Lección 3: Instalar paquetes](../integration-services/lesson-3-install-ssis-packages.md)  
  
  
  
