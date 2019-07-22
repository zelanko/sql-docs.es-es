---
title: default trace enabled (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], traces
- traces [SQL Server], logs
- default trace enabled option
ms.assetid: 1322d668-44f4-469e-8fd6-e0d02a81c8f2
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 33a04235580d70567b1de09180b10526255811bf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68011944"
---
# <a name="default-trace-enabled-server-configuration-option"></a>default trace enabled (opción de configuración del servidor)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Utilice la opción **default trace enabled** para habilitar o deshabilitar los archivos predeterminados de registro de seguimiento. La funcionalidad de registro de seguimiento predeterminado ofrece un registro completo y persistente de la actividad y los cambios principalmente relacionados con las opciones de configuración.  
  
> [!WARNING]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use eventos extendidos en su lugar.  
  
## <a name="purpose"></a>Finalidad  
 Los seguimientos predeterminados ofrecen ayuda para la solución de problemas a los administradores de bases de datos al garantizar que disponen de los datos de registro necesarios para diagnosticar los problemas la primera vez que ocurren.  
  
## <a name="viewing"></a>Ver  
 Los registros de seguimiento predeterminados se pueden abrir y examinar mediante [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] o se pueden consultar a través de [!INCLUDE[tsql](../../includes/tsql-md.md)] utilizando la función de sistema `fn_trace_gettable` . [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] puede abrir los archivos de registro de seguimiento predeterminados igual que si fueran archivos de salida de seguimiento normales. Los registros de seguimiento predeterminados se almacenan de forma predeterminada en el directorio `\MSSQL\LOG` mediante un archivo de seguimiento de sustitución. El nombre base del archivo predeterminado de registro de seguimiento es `log.trc`. En una instalación estándar de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el seguimiento predeterminado está habilitado y se transforma por tanto en TraceID 1. Si se habilita después de la instalación y después de crear otros seguimientos, el TraceID puede adoptar un número mayor.  
  
 Para obtener más información sobre el uso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler para ver este archivo de seguimiento, vea [Abrir un archivo de seguimiento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md)  
  
### <a name="example"></a>Ejemplo:  
 La instrucción siguiente abre el registro de seguimiento predeterminado en la ubicación predeterminada:  
  
```  
SELECT *   
FROM fn_trace_gettable  
('C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\LOG\log.trc', default);  
GO  
  
```  
  
## <a name="configuring"></a>Configuración  
 Si se selecciona el valor 1 para la opción **default trace enabled** , se habilita **Default Trace**. El valor predeterminado de esta opción es 1 (ON). El valor 0 desactiva el seguimiento.  
  
 **default trace enabled** es una opción avanzada. Si está usando el procedimiento almacenado del sistema **sp_configure** para cambiar la configuración, solo podrá cambiar la opción **Seguimiento predeterminado habilitado** cuando **Mostrar opciones avanzadas** esté configurado en 1. La configuración surte efecto inmediatamente, sin necesidad de reiniciar un servidor.  
  
## <a name="see-also"></a>Consulte también  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
