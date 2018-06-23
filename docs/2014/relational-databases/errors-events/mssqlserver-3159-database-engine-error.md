---
title: MSSQLSERVER_3159 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 3159 (Database Engine error)
ms.assetid: c93c1003-0e3a-40aa-9873-44a0f5b8b57e
caps.latest.revision: 16
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: cd227131e9d8e6449870f580c953b068a9b78152
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36200546"
---
# <a name="mssqlserver3159"></a>MSSQLSERVER_3159
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Identificador del evento|3159|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|LDDB_LOGNOTBACKEDUP|  
|Texto del mensaje|No se hizo copia del final del registro de la base de datos "%ls". Use BACKUP LOG WITH NORECOVERY para realizar una copia de seguridad del registro si contiene trabajo que no desea perder. Utilice la cláusula WITH REPLACE o WITH STOPAT de la instrucción RESTORE para sobrescribir el contenido del registro.|  
  
## <a name="explanation"></a>Explicación  
 En la mayoría de los casos, en los modelos de recuperación optimizado para cargas masivas de registros [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requiere que se realice una copia deL final del registro después del error para capturar las entradas del registro de las que todavía no se ha realizado una copia de seguridad. Una copia del final del registro que se realizan después del error, justo antes de una operación de restauración, se denominan copias del final del registro después del error.  
  
 Cuando se recupera una base de datos al momento en que se produjo el error, la copia del final del registro después del error es la última copia de seguridad de interés del plan de recuperación. Si no puede realizar una copia del final del registro después del error, puede recuperar una base de datos solo al final de la última copia de seguridad que se creó antes del error.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], por lo general, requiere que se realice una copia del final del registro después del error antes de comenzar a restaurar una base de datos. La copia del final del registro después del error evita la pérdida de trabajo y mantiene intacta la cadena de registros. Sin embargo, no todos los escenarios de restauración requieren una copia del final del registro después del error. No es necesario tener una copia del final del registro si el punto de recuperación está incluido en una copia de seguridad de registros anterior, o si está moviendo o reemplazando (sobrescribiendo) la base de datos y no necesita restaurarla a un momento después de la copia de seguridad más reciente. También, si los archivos de registro están dañados y no se puede crear una copia del final del registro, debe restaurar la base de datos sin utilizar una copia de seguridad de registros después del error. Las transacciones confirmadas después de la última copia de seguridad de registros se perderán. Para obtener más información, vea "Restaurar sin utilizar una copia del final del registro después del error" más adelante en este tema.  
  
> [!CAUTION]  
>  REPLACE no debe usarse a menudo y solo después de haberlo pensado detenidamente.  
  
## <a name="user-action"></a>Acción del usuario  
 Haga una copia del final del registro después del error y vuelva a intentar la operación de restauración.  
  
 Si no puede hacer una copia del final del registro después del error, utilice WITH STOPAT o WITH REPLACE en las instrucciones RESTORE.  
  
## <a name="see-also"></a>Vea también  
 [Restaurar una base de datos de SQL Server a un momento dado &#40;modelo de recuperación completa&#41;](../backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)   
 [Copia de seguridad del registro de transacciones cuando la base de datos está dañada &#40;SQL Server&#41;](../backup-restore/back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md)   
 [Realizar copia de seguridad de un registro de transacciones &#40;SQL Server&#41;](../backup-restore/back-up-a-transaction-log-sql-server.md)   
 [Copias del final del registro &#40;SQL Server&#41;](../backup-restore/tail-log-backups-sql-server.md)  
  
  