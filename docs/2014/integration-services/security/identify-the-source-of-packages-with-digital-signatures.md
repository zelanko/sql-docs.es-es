---
title: Identificar el origen de paquetes con firmas digitales | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- signing packages [Integration Services]
- certificates [Integration Services]
- packages [Integration Services], security
- security [Integration Services], certificates
- signing policies [Integration Services]
ms.assetid: a433fbef-1853-4740-9d5e-8a32bc4ffbb2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 714ede33a89a3ab4e44dae682887ee0c21c9f363
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62766657"
---
# <a name="identify-the-source-of-packages-with-digital-signatures"></a>Identificar el origen de paquetes con firmas digitales
  Es posible firmar un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] con un certificado digital para identificar su origen. Una vez que el paquete está firmado con un certificado digital, se puede configurar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para que compruebe la firma digital antes de cargarlo. Para hacer que [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] compruebe la firma, puede establecer una opción en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] o en la utilidad **dtexec** (dtexec.exe), o bien establecer un valor opcional del Registro.  
  
## <a name="signing-a-package-with-a-digital-certificate"></a>Firmar un paquete con un certificado digital  
 Antes de poder firmar un paquete con un certificado digital, debe obtener o crear el certificado. Cuando lo consiga, puede utilizar el certificado para firmar el paquete. Para obtener más información sobre cómo obtener un certificado y firmar un paquete con él, vea [Firmar un paquete mediante un certificado digital](../sign-a-package-by-using-a-digital-certificate.md).  
  
## <a name="setting-an-option-to-check-the-package-signature"></a>Establecer una opción para comprobar la firma del paquete  
 Tanto [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] como la utilidad **dtexec** tienen una opción que configura [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para que compruebe la firma digital de un paquete firmado. El uso de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] o de la utilidad **dtexec** depende de si desea comprobar todos los paquetes o simplemente algunos de ellos:  
  
-   Para comprobar la firma digital de todos los paquetes antes de cargarlos en tiempo de diseño, establezca la opción **Comprobar la firma digital al cargar un paquete** en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Esta opción es un valor de configuración global para todos los paquetes en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Para obtener más información, vea[página General](../general-page-of-integration-services-designers-options.md).  
  
-   Para comprobar la firma digital de un paquete concreto, especifique el `/VerifyS[igned]` opción cuando se usa el **dtexec** utilidad para ejecutar el paquete. Para más información, consulte [dtexec Utility](../packages/dtexec-utility.md).  
  
## <a name="setting-a-registry-value-to-check-the-package-signature"></a>Establecer un valor en el Registro para comprobar la firma del paquete  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] también admite un valor opcional del Registro, **BlockedSignatureStates**, que puede utilizarse para administrar la directiva de una organización para cargar los paquetes firmados y sin firmar. El valor del Registro puede evitar que los paquetes se carguen si están sin firmar o si tienen firmas que no sean válidas o de confianza. Para obtener más información sobre cómo establecer este valor del Registro, vea [Implementar una directiva de firma estableciendo un valor del Registro](../implement-a-signing-policy-by-setting-a-registry-value.md).  
  
> [!NOTE]  
>  El valor del Registro **BlockedSignatureStates** opcional puede especificar un parámetro de configuración más restrictivo que la opción de firma digital establecida en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] o en la línea de comandos de **dtexec** . En esta situación, el valor del Registro más restrictivo invalida los demás valores.  
  
## <a name="see-also"></a>Vea también  
 [Paquetes de Integration Services &#40;SSIS&#41;](../integration-services-ssis-packages.md)   
 [Información general sobre seguridad &#40;Integration Services&#41;](security-overview-integration-services.md)  
  
  
