---
title: Consideraciones de seguridad para las extensiones | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- security [Reporting Services], extensions
- extensions [Reporting Services], security
- permissions [Reporting Services], extensions
ms.assetid: 58cbdfeb-1105-4a7d-a3b8-b897ff95f367
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 128da8d5bb3b956b5b5661ce47ca6e4b741f0bc5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63282417"
---
# <a name="security-considerations-for-extensions"></a>Consideraciones de seguridad para las extensiones
  Cada aplicación que tenga como destino Common Language Runtime (CLR) debe interactuar con el sistema de seguridad de CLR. Cuando se ejecuta dicha aplicación, el CLR la evalúa automáticamente y le concede un conjunto de permisos. Según los permisos que reciba la aplicación, continúa ejecutándose o genera una excepción de seguridad. La configuración de seguridad local y las directivas de los archivos de configuración de la directiva de seguridad para un servidor de informes determinado definen los permisos de código que un ensamblado recibe.  
  
 Antes de solicitar los permisos, es necesario tener en cuenta los recursos y operaciones protegidas que se piensa usar en el código de la extensión y también saber qué permisos protegen esos recursos y operaciones. Además, se ha de realizar un seguimiento de los recursos a los que tienen acceso los métodos de bibliotecas de clases a los que llaman los componentes de la extensión. Para obtener más información, vea "Solicitar permisos" en la Guía del programador de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].  
  
 Las extensiones implementadas en un servidor de informes se deben ejecutar como de plena confianza, lo que significa que la extensión tiene que formar parte de un grupo de código al que se haya concedido el conjunto de permisos **FullTrust**. Esto también significa que la extensión puede tener acceso a ciertos recursos del servidor y operaciones disponibles a través del CLR, en función del usuario que se esté autenticando para un informe determinado. Para más información sobre grupos de código y extensiones, vea [Seguridad de acceso del código en Reporting Services](secure-development/code-access-security-in-reporting-services.md).  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] aplica la seguridad de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] para todas sus extensiones.  
  
 Las condiciones siguientes se aplican a la implementación de las extensiones de seguridad, procesamiento de datos, entrega y representación en [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]:  
  
-   Solo el administrador local tiene permiso para implementar una extensión.  
  
-   Solo los usuarios con los permisos de lectura/escritura adecuados pueden cambiar los archivos de configuración para el componente de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que se extiende.  
  
-   Solo los usuarios con privilegios tienen el permiso para modificar los archivos de directiva de seguridad y habilitar la seguridad de acceso del código para una extensión.  
  
 Para más información sobre la seguridad de acceso del código en [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], vea [Desarrollo seguro &#40;Reporting Services&#41;](secure-development/secure-development-reporting-services.md).  
  
 Para obtener más información sobre la seguridad de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], vea "Seguridad de .NET Framework" en la Guía del programador de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].  
  
## <a name="initialization-of-extension-assemblies"></a>Inicialización de los ensamblados de extensión  
 Cuando el servidor de informes carga por primera vez las extensiones en la memoria, utilizan las credenciales de cuenta de servicio, porque algunos ensamblados de extensión requieren permisos concretos para tener acceso a los recursos del sistema, leer los archivos de configuración y cargar otros ensamblados dependientes. Sin embargo, una vez cargado e inicializado un ensamblado, todas las llamadas subsiguientes a los ensamblados de extensión utilizan las credenciales de la cuenta de usuario en la que se ha iniciado sesión actualmente.  
  
## <a name="see-also"></a>Consulte también  
 [Extensiones de Reporting Services](reporting-services-extensions.md)   
 [Biblioteca de extensiones de Reporting Services](reporting-services-extension-library.md)  
  
  
