---
title: 'Lección 4: realizar una restauración a partir de una copia de seguridad completa de la base de datos | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: 580f76e6-9802-4abc-9043-db6de592c733
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: de9a356589ac6bceb532ed4cecf509f957e3c337
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "70153400"
---
# <a name="lesson-4-perform-a-restore-from-a-full-database-backup"></a>Lección 4: Realizar una restauración desde una copia de seguridad completa de la base de datos
  En esta lección se muestra el uso de una instrucción tsql para realizar una restauración desde una copia de seguridad completa de la base de datos creada en la lección anterior.  
  
## <a name="perform-a-restore-of-a-database-backup"></a>Realizar una restauración de una copia de seguridad de la base de datos  
 Para restaurar una copia de seguridad completa de la base de datos, siga estos pasos:  
  
1.  Conectarse a [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
2.  En el **Explorador de objetos**, conéctese a la instancia de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
3.  En el menú Estándar, haga clic en **Nueva consulta**.  
  
4.  Copie y pegue el ejemplo siguiente en la ventana de consulta, y modifíquelo como sea necesario.  
  
    ```  
    RESTORE DATABASE AdventureWorks2012   
    FROM URL = 'https://mystorageaccount.blob.core.windows.net/privatecontainertest/AdventureWorks2012.bak'   
    WITH CREDENTIAL = 'mycredential';  
    , STATS = 5 - use this to see monitor the progress  
    GO  
  
    ```  
  
5.  Compruebe la instrucción T-SQL y haga clic en **Ejecutar** .  
  
### <a name="return-to-tutorials-portal"></a>Volver al portal de tutoriales  
 [Tutorial: SQL Server copias de seguridad y restauración en Azure BLOB Storage Service](../relational-databases/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md).  
  
  
