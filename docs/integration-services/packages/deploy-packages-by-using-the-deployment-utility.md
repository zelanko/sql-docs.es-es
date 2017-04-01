---
title: "Implementar los paquetes mediante la utilidad de implementaci&#243;n | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "paquetes [Integration Services], instalar"
  - "instalar paquetes"
  - "dependencias [Integration Services]"
  - "implementar paquetes [Integration Services], instalar"
ms.assetid: eaf4b56e-2023-4d17-971c-703031da758c
caps.latest.revision: 57
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 57
---
# Implementar los paquetes mediante la utilidad de implementaci&#243;n
  Después de generar una utilidad de implementación para instalar paquetes de un proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en un equipo distinto del que se utilizó para generar la utilidad, debe copiar la carpeta de implementación en el equipo de destino.  
  
 La ruta de acceso a la carpeta de implementación se especifica en la propiedad DeploymentOutputPath del proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para el que ha creado la utilidad de implementación. La ruta predeterminada es bin\Deployment, relativa al proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Para más información, consulte [Create a Deployment Utility](../../integration-services/packages/create-a-deployment-utility.md).  
  
 Para instalar los paquetes, puede utilizar el Asistente para la instalación de paquetes. Para iniciar el asistente, haga doble clic en el archivo de la utilidad de implementación una vez copiada la carpeta de implementación en el servidor. El archivo recibe el nombre \<nombre del proyecto>.SSISDeploymentManifest, y se puede buscar en la carpeta de implementación del equipo de destino.  
  
> [!NOTE]  
>  Dependiendo de la versión del paquete que esté implementando, puede encontrar un error si tiene varias versiones diferentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instaladas en paralelo. Este error puede producirse porque la extensión de nombre de archivo .SSISDeploymentManifest es la misma para todas las versiones de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Al hacer doble clic en el archivo, se llama al instalador (dtsinstall.exe) para la versión instalada más recientemente de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], que podría no ser la misma versión que la del archivo de la utilidad de implementación. Para evitar este problema, ejecute la versión correcta de dtsinstall.exe desde la línea de comandos y proporcione la ruta de acceso al archivo de la utilidad de implementación.  
  
 El Asistente para la instalación de paquetes le guía paso a paso durante la instalación de paquetes en el sistema de archivos o en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Puede configurar la instalación de las maneras siguientes:  
  
-   Eligiendo el tipo de ubicación y la ubicación para instalar los paquetes.  
  
-   Eligiendo la ubicación para instalar las dependencias de paquete.  
  
-   Validando los paquetes una vez instalados en el servidor de destino.  
  
 Las dependencias basadas en archivos de los paquetes se instalan siempre en el sistema de archivos. Si instala un paquete en el sistema de archivos, las dependencias se instalarán en la misma carpeta que especificó para el paquete. Si instala un paquete en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede especificar la carpeta en la que desee almacenar las dependencias basadas en archivo.  
  
 Si el paquete incluye configuraciones que desea modificar para utilizarlas en el equipo de destino, puede utilizar el asistente para actualizar los valores de las propiedades.  
  
 Además de instalar paquetes con el Asistente para instalar paquetes, puede copiar y mover paquetes con la utilidad **dtutil** del símbolo del sistema. Para más información, consulte [dtutil Utility](../../integration-services/dtutil-utility.md).  
  
### Para implementar paquetes en una instancia de SQL Server  
  
1.  Abra la carpeta de implementación en el equipo de destino.  
  
2.  Haga doble clic en el archivo de manifiesto \<nombre del proyecto>.SSISDeploymentManifest para iniciar el Asistente para la instalación de paquetes.  
  
3.  En la página **Implementar paquetes SSIS** , seleccione la opción **Implementación en SQL Server** .  
  
4.  Opcionalmente, puede seleccionar **Validar los paquetes después de la instalación** para validar los paquetes una vez instalados en el servidor de destino.  
  
5.  En la página **Especificar el servidor SQL Server de destino** , especifique la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la que desee instalar los paquetes y seleccione un modo de autenticación. Si selecciona la Autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , deberá proporcionar un nombre de usuario y una contraseña.  
  
6.  En la página **Seleccionar la carpeta de instalación** , especifique la carpeta del sistema de archivos para las dependencias de paquete que se instalarán.  
  
7.  Si el paquete incluye configuraciones, puede modificarlas actualizando los valores de la lista **Valor** de la página Configurar paquetes.  
  
8.  Si elige validar los paquetes después de la instalación, vea los resultados de la validación de los paquetes implementados.  
  
## Vea también  
 [Implementación de paquetes heredada &#40;SSIS&#41;](../../integration-services/packages/legacy-package-deployment-ssis.md)  
  
  