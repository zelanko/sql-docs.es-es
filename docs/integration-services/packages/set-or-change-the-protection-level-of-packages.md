---
title: "Establecer o cambiar el nivel de protecci&#243;n de los paquetes | Microsoft Docs"
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
  - "contraseñas [Integration Services]"
  - "paquetes [Integration Services], seguridad"
  - "seguridad [Integration Services], niveles de protección"
  - "nivel de protección para paquetes [Integration Services]"
ms.assetid: 904a5580-82ba-4a26-b0c5-d1c989975f61
caps.latest.revision: 10
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 10
---
# Establecer o cambiar el nivel de protecci&#243;n de los paquetes
  Para controlar el acceso al contenido de los paquetes y a los valores confidenciales que contienen, como las contraseñas, establezca el valor de la propiedad **ProtectionLevel** . Los paquetes que se incluyen en un proyecto deben disponer del mismo nivel de protección que el proyecto con el fin de compilar el proyecto. Si cambia la configuración de las propiedades de **ProtectionLevel** en el proyecto, debe actualizar manualmente el valor de la propiedad de los paquetes.  
  
 Para obtener información sobre cómo determinar los valores de **ProtectionLevel** adecuados para los paquetes en las diferentes etapas del ciclo de vida de los paquetes, vea [Access Control for Sensitive Data in Packages](../../integration-services/packages/access-control-for-sensitive-data-in-packages.md). Para obtener información general sobre las características de seguridad de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], vea [Información general sobre seguridad &#40;Integration Services&#41;](../../integration-services/security/security-overview-integration-services.md).  
  
 Los procedimientos de este tema describen cómo utilizar [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] o la utilidad de símbolo del sistema dtutil para cambiar la propiedad **ProtectionLevel** .  
  
> [!NOTE]  
>  Además de los procedimientos de este tema, normalmente puede establecer o cambiar la propiedad **ProtectionLevel** de un paquete al importarlo o exportarlo. También puede cambiar la propiedad **ProtectionLevel** de un paquete al utilizar el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para guardarlo.  
  
### Para establecer o cambiar el nivel de protección de un paquete en herramientas de datos de SQL Server  
  
1.  Revise los valores disponibles para la propiedad **ProtectionLevel** en el tema [Configurar el nivel de protección de los paquetes](../../integration-services/packages/access-control-for-sensitive-data-in-packages.md)y determine el valor adecuado para su paquete.  
  
2.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el paquete.  
  
3.  Abra el paquete en el diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
4.  Si la ventana Propiedades no muestra las propiedades del paquete, haga clic en la superficie de diseño.  
  
5.  En la ventana Propiedades, en el grupo **Seguridad** , seleccione el valor adecuado para la propiedad **ProtectionLevel** .  
  
     Si selecciona un nivel de protección que requiere una contraseña, escríbala como valor de la propiedad **PackagePassword** .  
  
6.  En el menú **Archivo** , seleccione **Guardar los elementos seleccionados** para guardar el paquete modificado.  
  
### Para establecer o cambiar el nivel de protección de los paquetes en el símbolo del sistema  
  
1.  Revise los valores disponibles para la propiedad **ProtectionLevel** en el tema [Configurar el nivel de protección de los paquetes](../../integration-services/packages/access-control-for-sensitive-data-in-packages.md)y determine el valor adecuado para su paquete.  
  
2.  Revise las asignaciones para la opción **Encrypt** en el tema [dtutil Utility](../../integration-services/dtutil-utility.md)y determine el número entero adecuado que usar como valor de la propiedad **ProtectionLevel** seleccionada.  
  
3.  Abra una ventana de símbolo del sistema.  
  
4.  En el símbolo del sistema, navegue a la carpeta que contiene el paquete o paquetes para los que desea establecer la propiedad **ProtectionLevel** .  
  
     Los ejemplos de sintaxis mostrados en el paso siguiente suponen que esta carpeta es la actual.  
  
5.  Establezca o cambie el nivel de protección del paquete o paquetes utilizando un comando similar al de los ejemplos siguientes:  
  
    -   El comando siguiente establece la propiedad **ProtectionLevel** de un paquete individual en el sistema de archivos en el nivel 2, "Cifrado confidencial con contraseña", con la contraseña "strongpassword":  
  
         `dtutil.exe /file "C:\Package.dtsx" /encrypt file;"C:\Package.dtsx";2;strongpassword`  
  
    -   El comando siguiente establece la propiedad **ProtectionLevel** de todos los paquetes en una carpeta concreta del sistema de archivos en el nivel 2, "Cifrado confidencial con contraseña", con la contraseña "strongpassword":  
  
         `for %f in (*.dtsx) do dtutil.exe /file %f /encrypt file;%f;2;strongpassword`  
  
         Si utiliza un comando similar en un archivo por lotes, escriba el marcador de posición del archivo, "% f", como "%% f" en el archivo por lotes.  
  
## Vea también  
 [dtutil (utilidad)](../../integration-services/dtutil-utility.md)  
  
  