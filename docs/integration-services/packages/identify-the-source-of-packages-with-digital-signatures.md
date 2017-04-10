---
title: "Identificar el origen de paquetes con firmas digitales | Microsoft Docs"
ms.custom: ""
ms.date: "08/24/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "firmar paquetes [Integration Services]"
  - "conexiones [Integration Services]"
  - "paquetes [Integration Services], seguridad"
  - "seguridad [Integration Services], certificados"
  - "directivas de firma [Integration Services]"
ms.assetid: a433fbef-1853-4740-9d5e-8a32bc4ffbb2
caps.latest.revision: 46
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 46
---
# Identificar el origen de paquetes con firmas digitales
  Es posible firmar un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] con un certificado digital para identificar su origen. Una vez que el paquete está firmado con un certificado digital, se puede configurar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para que compruebe la firma digital antes de cargarlo. Para hacer que [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] compruebe la firma, puede establecer una opción en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] o en la utilidad **dtexec** (dtexec.exe), o bien establecer un valor opcional del Registro.  
  
## Firmar un paquete con un certificado digital  
 Antes de poder firmar un paquete con un certificado digital, debe obtener o crear el certificado. Cuando lo consiga, puede utilizar el certificado para firmar el paquete. Para obtener más información sobre cómo obtener un certificado y firmar un paquete con él, vea [Firmar un paquete mediante un certificado digital](../../integration-services/packages/sign-a-package-by-using-a-digital-certificate.md).  
  
## Establecer una opción para comprobar la firma del paquete  
 Tanto [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] como la utilidad **dtexec** tienen una opción que configura [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para que compruebe la firma digital de un paquete firmado. El uso de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] o de la utilidad **dtexec** depende de si desea comprobar todos los paquetes o simplemente algunos de ellos:  
  
-   Para comprobar la firma digital de todos los paquetes antes de cargarlos en tiempo de diseño, establezca la opción **Comprobar la firma digital al cargar un paquete** en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Esta opción es un valor de configuración global para todos los paquetes en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].
  
-   Para comprobar la firma digital de un paquete concreto, especifique la opción **/VerifyS[igned]** al usar la utilidad **dtexec** para ejecutar el paquete. Para más información, consulte [dtexec Utility](../../integration-services/packages/dtexec-utility.md).  
  
## Establecer un valor del Registro para comprobar la firma del paquete  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] también admite un valor opcional del Registro, **BlockedSignatureStates**, que puede utilizarse para administrar la directiva de una organización para cargar los paquetes firmados y sin firmar. El valor del Registro puede evitar que los paquetes se carguen si están sin firmar o si tienen firmas que no sean válidas o de confianza. Para obtener más información sobre cómo establecer este valor del Registro, vea [Implementar una directiva de firma estableciendo un valor del Registro](../../integration-services/packages/implement-a-signing-policy-by-setting-a-registry-value.md).  
  
> **NOTA:** El valor del Registro **BlockedSignatureStates** opcional puede especificar un parámetro de configuración más restrictivo que la opción de firma digital establecida en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] o en la línea de comandos de **dtexec**. En esta situación, el valor del Registro más restrictivo invalida los demás valores.  
  
## Vea también  
 [Paquetes de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-packages.md)   
 [Información general sobre seguridad &#40;Integration Services&#41;](../../integration-services/security/security-overview-integration-services.md)  
  
  