---
title: Opciones de línea de comandos de la herramienta de administración (utilidad Distributed Replay) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: c01b0ed3-67e4-4561-92d2-a8fbb086aca8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f53c456832e89aa96c0f7c9a1decd9fabbe96360
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52815967"
---
# <a name="administration-tool-command-line-options-distributed-replay-utility"></a>Opciones de línea de comandos de la herramienta de administración (utilidad Distributed Replay)
  El [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herramienta de administración de Distributed Replay, `DReplay.exe`, es una herramienta de línea de comandos que puede usar para comunicarse con distributed replay controller. Utilice la herramienta de administración para iniciar, supervisar y cancelar operaciones en el controlador.  
  
 ![Icono de vínculo de tema](../../database-engine/media/topic-link.gif "Icono de vínculo de tema") Para obtener más información sobre las convenciones de sintaxis que se usan con la sintaxis de la herramienta de administración, vea [Convenciones de sintaxis de Transact-SQL &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/transact-sql-syntax-conventions-transact-sql).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
      dreplay {preprocess|replay|status|cancel} [options] [-?]}  
  
Usage:  
  
  dreplay preprocess [-mcontroller] -iinput_trace_file  
    -dcontroller_working_dir [-cconfig_file] [-fstatus_interval]  
  
  dreplay replay [-mcontroller] -dcontroller_working_dir [-o]  
    [-starget_server] -wclients [-cconfig_file]  
    [-fstatus_interval]  
  
  dreplay status [-mcontroller] [-fstatus_interval]  
  
  dreplay cancel [-mcontroller] [-q]   
```  
  
## <a name="remarks"></a>Comentarios  
 Puede emitir las siguientes opciones de línea de comandos con `DReplay.exe`:  
  
 **preprocess**  
 Inicia la fase de preprocesamiento. El controlador prepara la información de seguimiento de entrada, que se capturó en el entorno de producción, para la reproducción en el servidor de destino.  
  
 **reproducir**  
 Inicia la fase de reproducción de eventos. El controlador envía los datos de la reproducción a los clientes especificados, inicia la reproducción distribuida y sincroniza los clientes. Opcionalmente, cada cliente que se ha seleccionado registra la actividad de reproducción y guarda los archivos de seguimiento del resultado localmente.  
  
 **status**  
 Consulta el controlador y muestra el estado actual.  
  
 **cancel**  
 Cancela la operación que se está ejecutando actualmente en el controlador.  
  
 Para obtener información de la sintaxis detallada que incluye los argumentos de comando y ejemplos, vea los siguientes temas:  
  
-   [Opción de preprocesamiento &#40;herramienta de administración Distributed Replay&#41;](preprocess-option-distributed-replay-administration-tool.md)  
  
-   [Opción Replay &#40;herramienta de administración Distributed Replay&#41;](replay-option-distributed-replay-administration-tool.md)  
  
-   [Opción Status &#40;herramienta de administración de Distributed Replay&#41;](status-option-distributed-replay-administration-tool.md)  
  
-   [Opción cancel &#40;herramienta de administración de Distributed Replay&#41;](cancel-option-distributed-replay-administration-tool.md)  
  
 Las RPC se reproducen como RPC y no como eventos de lenguaje.  
  
## <a name="permissions"></a>Permisos  
 Debe ejecutar la herramienta de administración como un usuario interactivo, como un usuario local o una cuenta de usuario de dominio. Para utilizar una cuenta de usuario local, la herramienta de administración y el controlador se deben estar ejecutando en el mismo equipo.  
  
 Para más información, consulte [Distributed Replay Security](distributed-replay-security.md).  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Distributed Replay](sql-server-distributed-replay.md)  
  
  
