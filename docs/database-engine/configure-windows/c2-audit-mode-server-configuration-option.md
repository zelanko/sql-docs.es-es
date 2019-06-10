---
title: c2 audit mode (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
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
manager: jroth
ms.openlocfilehash: 2b962821437013f6aa086d472e284ed0fef21138
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66799559"
---
# <a name="c2-audit-mode-server-configuration-option"></a>c2 audit mode (opción de configuración del servidor)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  El modo auditoría C2 puede configurarse mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o con la opción **Modo auditoría C2** de **sp_configure**. Al seleccionar esta opción, el servidor registrará tanto los intentos sin éxito como los intentos con éxito de acceso a instrucciones y objetos. Esta información puede servirle de ayuda para perfilar la actividad del sistema y realizar un seguimiento de las posibles infracciones de las directivas de seguridad.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] El estándar de seguridad C2 se ha sustituido por Common Criteria Certification. Vea [common criteria compliance enabled (opción de configuración del servidor)](../../database-engine/configure-windows/common-criteria-compliance-enabled-server-configuration-option.md).  
  
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
  
## <a name="see-also"></a>Consulte también  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
