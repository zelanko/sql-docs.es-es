---
title: Establecer o cambiar el nivel de protección de paquetes | Documentos de Microsoft
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- passwords [Integration Services]
- packages [Integration Services],security
- security [Integration Services],protection levels
- protection level for packages [Integration Services]
ms.assetid: 904a5580-82ba-4a26-b0c5-d1c989975f61
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 695667f3ba50b6cde3d2b9629e7116fecf7c4b16
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36200573"
---
# <a name="set-or-change-the-protection-level-of-packages"></a>Establecer o cambiar el nivel de protección de los paquetes
  Para controlar el acceso al contenido de los paquetes y a los valores confidenciales que contienen, como las contraseñas, establezca el valor de la propiedad `ProtectionLevel`. Los paquetes que se incluyen en un proyecto deben disponer del mismo nivel de protección que el proyecto con el fin de compilar el proyecto. Si cambia la configuración de las propiedades de `ProtectionLevel` en el proyecto, debe actualizar manualmente el valor de la propiedad de los paquetes.  
  
 Para obtener información sobre cómo determinar la `ProtectionLevel` valores que son adecuados para los paquetes en las diferentes etapas en el ciclo de vida del paquete, vea [Control de acceso para los datos confidenciales en paquetes](security/access-control-for-sensitive-data-in-packages.md). Para obtener información general sobre las características de seguridad de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], vea [Información general sobre seguridad &#40;Integration Services&#41;](security/security-overview-integration-services.md).  
  
 Los procedimientos descritos en este tema describen cómo utilizar [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] o la utilidad de símbolo del sistema dtutil para cambiar la `ProtectionLevel` propiedad.  
  
> [!NOTE]  
>  Además de los procedimientos de este tema, normalmente puede establecer o cambiar la `ProtectionLevel` propiedad de un paquete al importar o exportar el paquete. También puede cambiar la propiedad `ProtectionLevel` de un paquete al utilizar el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para guardarlo.  
  
### <a name="to-set-or-change-the-protection-level-of-a-package-in-sql-server-data-tools"></a>Para establecer o cambiar el nivel de protección de un paquete en herramientas de datos de SQL Server  
  
1.  Revise los valores disponibles para la `ProtectionLevel` propiedad en el tema [configurar el nivel de protección de paquetes](security/access-control-for-sensitive-data-in-packages.md)y determine el valor adecuado para el paquete.  
  
2.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete.  
  
3.  Abra el paquete en el diseñador de [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
4.  Si la ventana Propiedades no muestra las propiedades del paquete, haga clic en la superficie de diseño.  
  
5.  En la ventana Propiedades, en la **seguridad** grupo, seleccione el valor adecuado para la `ProtectionLevel` propiedad.  
  
     Si selecciona un nivel de protección que requiere una contraseña, escríbala como valor de la propiedad **PackagePassword** .  
  
6.  En el menú **Archivo** , seleccione **Guardar los elementos seleccionados** para guardar el paquete modificado.  
  
### <a name="to-set-or-change-the-protection-level-of-packages-at-the-command-prompt"></a>Para establecer o cambiar el nivel de protección de los paquetes en el símbolo del sistema  
  
1.  Revise los valores disponibles para la `ProtectionLevel` propiedad en el tema [configurar el nivel de protección de paquetes](security/access-control-for-sensitive-data-in-packages.md)y determine el valor adecuado para el paquete.  
  
2.  Revise las asignaciones para el `Encrypt` opción en el tema [dtutil (utilidad)](dtutil-utility.md)y determine el número entero adecuado que se usará como el valor de seleccionado `ProtectionLevel` propiedad.  
  
3.  Abra una ventana de símbolo del sistema.  
  
4.  En el símbolo del sistema, navegue hasta la carpeta que contiene el paquete o paquetes para el que desea establecer el `ProtectionLevel` propiedad.  
  
     Los ejemplos de sintaxis mostrados en el paso siguiente suponen que esta carpeta es la actual.  
  
5.  Establezca o cambie el nivel de protección del paquete o paquetes utilizando un comando similar al de los ejemplos siguientes:  
  
    -   El comando siguiente establece la `ProtectionLevel` propiedad de un paquete individual en el sistema de archivos al nivel 2, "Cifrado confidencial con contraseña", con la contraseña "strongpassword":  
  
         `dtutil.exe /file "C:\Package.dtsx" /encrypt file;"C:\Package.dtsx";2;strongpassword`  
  
    -   El comando siguiente establece la propiedad `ProtectionLevel` de todos los paquetes en una carpeta concreta del sistema de archivos en el nivel 2, "Cifrado confidencial con contraseña", con la contraseña "strongpassword":  
  
         `for %f in (*.dtsx) do dtutil.exe /file %f /encrypt file;%f;2;strongpassword`  
  
         Si utiliza un comando similar en un archivo por lotes, escriba el marcador de posición del archivo, "% f", como "%% f" en el archivo por lotes.  
  
## <a name="see-also"></a>Vea también  
 [dtutil (utilidad)](dtutil-utility.md)  
  
  