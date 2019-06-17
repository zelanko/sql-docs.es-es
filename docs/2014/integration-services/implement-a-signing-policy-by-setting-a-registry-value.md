---
title: Implementar una directiva de firma estableciendo un valor del registro | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- signing policies [Integration Services]
ms.assetid: 64f6966f-2292-401f-acb1-2ccb5aee484a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 21bda8729c30df9493c4f969c5af05b6dd80386f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66058215"
---
# <a name="implement-a-signing-policy-by-setting-a-registry-value"></a>Implementar una directiva de firma estableciendo un valor del Registro
  Se puede usar un valor opcional del Registro para administrar la directiva de una organización para la carga de paquetes firmados o sin firmar. Si utiliza este valor del Registro, debe crearlo en cada equipo en el que se ejecutarán los paquetes de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] y en el que desea exigir el cumplimiento de la directiva. Una vez establecido el valor del Registro, [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] comprobará las firmas antes de cargar los paquetes.  
  
 En este procedimiento de este tema se describe cómo agregar el valor DWORD opcional `BlockedSignatureStates` a la clave del Registro HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS. El valor de los datos de `BlockedSignatureStates` determina si se debe bloquear un paquete que tenga una firma que no sea de confianza, una firma no válida, o que esté sin firmar. Con respecto al estado de las firmas que se utilizan para firmar paquetes, el valor del Registro `BlockedSignatureStates` usa las siguientes definiciones:  
  
-   Una *firma válida* es una firma que puede leerse correctamente.  
  
-   Una *firma no válida* es una firma para la que la suma de comprobación descifrada (algoritmo hash unidireccional del código de paquete cifrado con una clave privada) no coincide con la suma de comprobación descifrada que se calcula como parte del proceso de carga de paquetes de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
-   Una *firma de confianza* es una firma creada mediante un certificado digital firmado por una entidad de certificación raíz de confianza. Este valor de configuración no exige que el firmante se encuentre en la lista de publicadores de confianza del usuario.  
  
-   Una *firma que no es de confianza* es una firma que no se puede comprobar que haya sido emitida por una entidad de certificación raíz de confianza o una firma que no es actual.  
  
 En la tabla siguiente se enumeran los valores válidos de los datos DWORD y su directiva asociada.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|0|Sin restricción administrativa.|  
|1|Bloquear firmas no válidas.<br /><br /> Este valor no bloquea los paquetes sin firmar.|  
|2|Bloquear las firmas no válidas y las que no sean de confianza.<br /><br /> Este valor no bloquea los paquetes sin firmar, pero bloquea las firmas generadas automáticamente.|  
|3|Bloquear las firmas no válidas, las que no sean de confianza y los paquetes sin firmar.<br /><br /> Este valor también bloquea las firmas generadas automáticamente.|  
  
> [!NOTE]  
>  El valor recomendado para `BlockedSignatureStates` es 3. Este valor proporciona la protección óptima frente a paquetes sin firmar o firmas que no son válidas o no son de confianza. No obstante, es posible que el valor recomendado no sea adecuado para todas las circunstancias. Para obtener más información sobre la firma de activos digitales, vea el tema de[introducción a la firma de código](https://go.microsoft.com/fwlink/?LinkId=51414)en MSDN Library.  
  
### <a name="to-implement-a-signing-policy-for-packages"></a>Para implementar una directiva de firma para paquetes  
  
1.  En el menú **Inicio** , haga clic en **Ejecutar**.  
  
2.  En el cuadro de diálogo Ejecutar, escriba `Regedit`y, a continuación, haga clic en **Aceptar**.  
  
3.  Busque la clave del Registro HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS.  
  
4.  Haga clic con el botón derecho en **MSDTS**, seleccione **Nuevo**y, después, haga clic en **Valor DWORD**.  
  
5.  Actualice el nombre del nuevo valor a `BlockedSignatureStates`.  
  
6.  Haga clic en `BlockedSignatureStates` y haga clic en **modificar**.  
  
7.  En el cuadro de diálogo **Editar valor DWORD** , escriba el valor 0, 1, 2 o 3.  
  
8.  Haga clic en **Aceptar**.  
  
9. En el menú **Archivo** , haga clic en **Salir**.  
  
## <a name="see-also"></a>Vea también  
 [Información general sobre seguridad &#40;Integration Services&#41;](security/security-overview-integration-services.md)   
 [Identificar el origen de paquetes con firmas digitales](security/identify-the-source-of-packages-with-digital-signatures.md)  
  
  
