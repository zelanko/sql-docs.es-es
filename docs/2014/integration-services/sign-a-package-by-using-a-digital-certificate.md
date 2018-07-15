---
title: Firmar un paquete mediante un certificado Digital | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- digital signatures [Integration Services]
- signing packages [Integration Services]
- signatures [Integration Services]
ms.assetid: 182b115e-0fe2-4717-8dff-183f9eb6e397
caps.latest.revision: 59
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 011b4ee289a55f150d7a800a26db2f9f7f954ad0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37326235"
---
# <a name="sign-a-package-by-using-a-digital-certificate"></a>Firmar un paquete mediante un certificado digital
  En este tema se describe cómo firmar un paquete de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] con un certificado digital. Puede utilizar una firma digital, junto con otros valores de configuración, para evitar que se cargue y se ejecute un paquete que no es válido.  
  
 Antes de poder firmar un paquete de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] debe realizar las tareas siguientes:  
  
-   Crear u obtener una clave privada para asociarla al certificado y almacenarla en el equipo local.  
  
-   Obtener un certificado para firmar código de una entidad de certificación de confianza. Puede utilizar uno de los métodos siguientes para obtener o crear un certificado:  
  
    -   Obtener un certificado de una entidad de certificación pública comercial que se dedique a emitirlos.  
  
    -   Obtener un certificado de un servidor de certificados que permita a una organización emitir certificados internamente. Tiene que agregar el certificado raíz utilizado para firmar dicho certificado al almacén **Entidades de certificación raíz de confianza** . Para ello, puede utilizar el complemento Certificados de [!INCLUDE[msCoName](../includes/msconame-md.md)] Management Console (MMC). Para obtener más información, vea el tema "[Certificate Services](http://go.microsoft.com/fwlink/?LinkId=100755)" en MSDN Library.  
  
    -   Crear su propio certificado solo con fines de pruebas. La herramienta Creación de certificados (Makecert.exe) genera certificados X.509 solo a efectos de pruebas. Para obtener más información, vea el tema "[Herramienta Creación de certificados (Makecert.exe)](http://go.microsoft.com/fwlink/?LinkId=100756)" en MSDN Library.  
  
     Para obtener más información sobre los certificados, vea la Ayuda en pantalla para el complemento Certificados. Para obtener más información sobre cómo firmar activos digitales, vea el tema "[Signing and Checking Code with Authenticode](http://go.microsoft.com/fwlink/?LinkId=78100)" en MSDN Library.  
  
-   Asegurarse de que el certificado se ha habilitado para la firma de código. Para determinar si un certificado está habilitado para la firma de código, revise las propiedades del certificado en el complemento Certificados.  
  
-   Almacenar el certificado en el almacén personal.  
  
 Una vez completadas las tareas anteriores, puede utilizar el procedimiento siguiente para firmar un paquete.  
  
### <a name="to-sign-a-package"></a>Para firmar un paquete  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete que debe firmarse.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  En el Diseñador de [!INCLUDE[ssIS](../includes/ssis-md.md)] , en el menú **SSIS** , haga clic en **Firma digital**.  
  
4.  En el cuadro de diálogo **Firma digital** , haga clic en **Firmar**.  
  
5.  En el cuadro de diálogo **Seleccionar el certificado** , seleccione un certificado.  
  
6.  (Opcional) Haga clic en **Ver certificado**para ver la información del certificado.  
  
7.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Seleccionar un certificado** .  
  
8.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Firma digital** .  
  
9. Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados** , en el menú **Archivo** .  
  
     Aunque se haya firmado el paquete, también debe configurar [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] para comprobar la firma digital antes de cargar el paquete. Para más información, vea [Identificar el origen de paquetes con firmas digitales](security/identify-the-source-of-packages-with-digital-signatures.md).  
  
## <a name="see-also"></a>Vea también  
 [Información general sobre seguridad &#40;Integration Services&#41;](security/security-overview-integration-services.md)  
  
  
