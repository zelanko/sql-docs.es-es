---
title: "Espacio en disco del registro de transacciones para operaciones de índice | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: indexes
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-indexes
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- index disk space [SQL Server]
- space [SQL Server], indexes
- transaction logs [SQL Server], disk space
- disk space [SQL Server], transaction logs
- space [SQL Server], transaction logs
ms.assetid: 4f8a4922-4507-4072-be67-c690528d5c3b
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7fcf3131776066e183f0b6f031dce00d143bdeca
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2018
---
# <a name="transaction-log-disk-space-for-index-operations"></a>Espacio en disco del registro de transacciones para operaciones de índice
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Las operaciones de índice a gran escala pueden generar cargas grandes de datos que podrían llenar rápidamente el registro de transacciones. Para estar seguros de que la operación de índice se pueda revertir, el registro de transacciones no se puede truncar hasta que se haya completado la operación de índice; no obstante, se puede realizar una copia de seguridad del registro durante la operación de índice. Por lo tanto, el registro de transacciones debe tener suficiente espacio para almacenar las transacciones de la operación de índice y cualquier transacción de usuario simultánea durante la operación de índice. Esto se cumple para las operaciones de índice en línea y sin conexión. Debido a que no es posible obtener acceso a las tablas subyacentes durante una operación de índice sin conexión, puede que haya pocas transacciones de usuario y el registro no crezca tan rápidamente. Las operaciones de índice en línea no impiden la actividad simultánea de usuarios, por lo tanto, las operaciones de índice en línea a gran escala junto con un número significativo de transacciones simultáneas pueden provocar el crecimiento continuo del registro de transacciones sin la posibilidad de truncar el registro.  
  
## <a name="recommendations"></a>Recomendaciones  
 Cuando ejecute operaciones de índice a gran escala, tenga en cuentas las siguientes recomendaciones:  
  
1.  Compruebe que se ha realizado una copia de seguridad del registro de transacciones y que éste se ha truncado antes de ejecutar operaciones de índice a gran escala en línea, así como que el registro dispone de espacio suficiente para almacenar el índice proyectado y las transacciones de usuario.  
  
2.  Considere la posibilidad de establecer la opción SORT_IN_TEMPDB en ON para la operación de índice. De este modo, se separan las transacciones de índice de transacciones de usuario simultáneas. Las transacciones de índice se almacenarán en el registro de transacciones de **tempdb** y las transacciones de usuario simultáneas se almacenarán en el registro de transacciones de la base de datos de usuario. Esto permite que el registro de transacciones de la base de datos de usuario se trunque durante la operación de índice si es necesario. Además, si el registro de **tempdb** no se encuentra en el mismo disco que el registro de la base de datos de usuario, los dos registros no compiten por el mismo espacio en disco.  
  
    > [!NOTE]  
    >  Compruebe que la base de datos **tempdb** y el registro de transacciones disponen de espacio suficiente para controlar la operación de índice. El registro de transacciones de **tempdb** no se puede truncar hasta que finalice la operación de índice.  
  
3.  Utilice un modelo de recuperación de base de datos que permita el registro mínimo de la operación de índice. Esto puede reducir el tamaño del registro e impide que el registro llene el espacio de registro.  
  
4.  No ejecute la operación de índice en línea en una transacción explícita. El registro no se truncará hasta que finalice la operación explícita.  
  
## <a name="related-content"></a>Contenido relacionado  
 [Requisitos de espacio en disco para operaciones DDL de índice](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md)  
  
 [Ejemplo de espacio en disco del índice](../../relational-databases/indexes/index-disk-space-example.md)  
  
  
