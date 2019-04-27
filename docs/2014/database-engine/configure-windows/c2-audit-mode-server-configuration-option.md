---
title: c2 audit mode (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- auditing [SQL Server]
- audits [SQL Server], C2 Audit Mode option
- C2 auditing
- C2 Audit Mode option
- recording attempts
ms.assetid: 5a8d73a6-c4f6-4967-ba11-ecbcfc90b9cc
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0233f6c40e15fd4f612002854477d98068901b15
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62786674"
---
# <a name="c2-audit-mode-server-configuration-option"></a>c2 audit mode (opción de configuración del servidor)
  El modo auditoría C2 puede configurarse mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o con la opción **Modo auditoría C2** de **sp_configure**. Al seleccionar esta opción, el servidor registrará tanto los intentos sin éxito como los intentos con éxito de acceso a instrucciones y objetos. Esta información puede servirle de ayuda para perfilar la actividad del sistema y realizar un seguimiento de las posibles infracciones de las directivas de seguridad.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] El estándar de seguridad C2 se ha sustituido por Common Criteria Certification. Vea [common criteria compliance enabled (opción de configuración del servidor)](common-criteria-compliance-enabled-server-configuration-option.md).  
  
## <a name="audit-log-file"></a>Archivo de registro de auditoría  
 Los datos del modo auditoría C2 se guardan en un archivo en el directorio de datos predeterminado de la instancia. Si el tamaño del archivo de registro de auditoría supera el límite de 200 megabytes (MB), [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] creará un archivo nuevo, cerrará el antiguo y escribirá todos los registros de auditoría nuevos en el nuevo archivo. Este proceso continuará hasta que el directorio de datos de auditoría se llene o la función de auditoría se desactive. Para determinar el estado de un seguimiento de C2, consulte la vista de catálogo sys.traces.  
  
> [!IMPORTANT]  
>  El modo auditoría C2 guarda una gran cantidad de información de eventos en el archivo de registro, por lo que puede crecer rápidamente. Si el directorio de datos en el que se guardan los registros se queda sin espacio, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se cerrará automáticamente. Si la auditoría se ha configurado para iniciarse automáticamente, deberá reiniciar la instancia con la marca **-f** (que omite la auditoría) o liberar más espacio en disco para el registro de auditoría.  
  
## <a name="permissions"></a>Permisos  
 Requiere la pertenencia al rol fijo de servidor **sysadmin** .  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente activa el modo auditoría C2.  
  
```  
sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE ;  
GO  
  
sp_configure 'c2 audit mode', 1 ;  
GO  
RECONFIGURE ;  
GO  
  
```  
  
## <a name="see-also"></a>Vea también  
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
